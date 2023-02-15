# Authorization system<a name="chapter-authorization"></a>

You can use the EnginFrame Authorization System to control which *users* can access the EnginFrame *resources* based on policies that you set\. Through these policies, you can grant or deny a user access to specific resources or to do specific operations\. 

In the EnginFrame Authorization System, *users* and *groups* are called Actors, *resources* are divided into EnginFrame service definition files \(SDF\) folders, services, service options, service actions and service output, and the *policies* define the permissions that are specified using access control lists \(ACL\)\. 

The authorization framework defines *who* can do *what* on *which resources*\. By configuring the authorization system, you can give different views of the EnginFrame Portal to different users and user groups\. 

## Configuring authorization<a name="authorization-config"></a>

EnginFrame authorization settings are specified in the following configuration files\. The ACLs and Actors that are defined in all of them are merged\. If there are multiple definitions of the same ACLs or Actors, the following file priority is used to resolve conflicts, from highest to lowest priority\.
+ `$EF_TOP/conf/enginframe/authorization.xconf` \(highest priority\)
+ `$EF_TOP/<VERSION>/enginframe/conf/authorization.xconf` \(medium priority\)
+ `$EF_TOP/conf/plugins/<plug-in>/authorization.xconf` \(low priority\)
+ `$EF_TOP/<VERSION>/enginframe/plugins/<plug-in>/conf/authorization.xconf` \(lowest priority\)

Modifications to these files are automatically picked up by a running EnginFrame Server, without requiring a restart\. 

The `authorization.xconf` file is an XML file consisting of two sections:
+  An *Actors* section that's introduced with the tag `<ef:acl-actor-list>` 
+  An *Access Control Lists* section that starts with the tag `<ef:acl-list>` 

```
<ef:authorization>
       <!-- EnginFrame Authorization Actors section -->
       <ef:acl-actor-list>
           ...
       </ef:acl-actor-list>
       <!-- EnginFrame Authorization ACL section -->
       <ef:acl-list>
           ...
       </ef:acl-list>
</ef:authorization>
```

**Topics**
+ [Defining Actors](#defining-actors)
+ [Defining access control lists](#defining-acl)
+ [Condition based ACL](#conditionBased-ACL)

### Defining Actors<a name="defining-actors"></a>

Actors are entities that can perform actions on resources\. In the EnginFrame infrastructure an Actor can be a user, a group of users, or a group of groups of users\. 

Because an Actor can be a single user or a group, we refer to each component using the term *member*\. 

There are three ways to define an Actor:
+  *efgroup Actor* is an explicit list of members\. It can contain one or more users or even other Actors already defined\. 
+  *osgroup Actor* is a list of members that includes the users that belong to the Operating System group that also has the same ID as the Actors associated with it\.
+  *user Actor* is an actor for a single EnginFrame user\. It exists just for "renaming" purposes because usually there's no need to wrap an EnginFrame user ID in an Actor\. 

The XML syntax that's used to define Actors inside `authorization.xconf` config file is as follows:

```
<ef:acl-actor id="unique_id” type="efgroup|osgroup">
```

An Actor of type `efgroup` must include members defined with the following:

```
<ef:acl-member type="efuser|acl-actor">...</ef:acl-member>
```

**Note**  
When using a member of the `acl-actor` type, the Actor must be defined in the `authorization.xconf` config file\. 

The following is an Actors section example:

```
...
<!-- EnginFrame Authorization Actors section -->
<ef:acl-actor-list>
  <!-- Actor made up of two simple users and two Actors -->
  <ef:acl-actor id="nice" type="efgroup">
     <ef:info>NICE people</ef:info>
     <ef:acl-member type="efuser">andrea</ef:acl-member>
     <ef:acl-member type="efuser">beppe</ef:acl-member>
     <ef:acl-member type="acl-actor">
        developers
     </ef:acl-member>
     <ef:acl-member type="acl-actor">efadmin</ef:acl-member>
  </ef:acl-actor>
  <ef:acl-actor id="developers" type="efgroup">
     <ef:info>EnginFrame Developers</ef:info>
     <ef:acl-member type="efuser">antonio</ef:acl-member>
     <ef:acl-member type="efuser">mauri</ef:acl-member>
     <ef:acl-member type="acl-actor">goldrake</ef:acl-member>
  </ef:acl-actor>
  <!--
    Member of this Actor are dynamically loaded from the
    Operating system group “efadmin” using the script:
    NICE_ROOT/enginframe/plugins/myplugin/bin/ef.load.users
    -->
  <ef:acl-actor id="efadmin" type="osgroup" plugin="myplugin"/>
</ef:acl-actor-list>
...
```

### Defining access control lists<a name="defining-acl"></a>

Access control lists \(ACL\) define policies that are applied to Actors when they try to perform actions on resources\. 

The purpose of an access control list \(ACL\) is to grant or deny permissions on actions that an EnginFrame Actor can perform without reference to a specific resource\. 

An ACL consists of three main parts\. The first section is used to "bias" the ACL towards the `allow` or the `deny` directive\. The following two parts define the allow and deny directives where Actors are bound with the actions they can or cannot perform\. 

The ACL structure explanation follows 
+ *ACL priority*, defines if the allow or deny directive has priority for this ACL:
  + `allow` priority: By default, access is allowed\. The deny directives are evaluated before the allow ones\. Any Actor that doesn't match a deny directive or matches an allow directive is allowed access to the resource\.
  + `deny` priority: By default, access is denied\. The allow directives are evaluated before the deny ones\. Any Actor that doesn't match an allow directive or matches a deny directive is denied access to the resource\.
+ *ACL allow*, contains the allow directives, a list of Actors where a set of actions specifies the operations that the Actor can actually perform on a generic resource guarded by this ACL\. 
+ *ACL deny*, contains the deny directives, a list of Actors where a set of actions specifies the operations that the Actor can't perform on a generic resource guarded by this ACL\. 

The definition of an ACL adheres to this XML structure:

```
...
  <ef:acl id="unique_id”>
    <ef:acl-priority>allow | deny</ef:acl-priority>
    <ef:acl-allow>
      <ef:actor id=”actor_id”>
        <ef:action-list>
          <ef:read/>
          <ef:execute/>
          ...
        </ef:action-list>
      </ef:actor>
    </ef:acl-allow>
    <ef:acl-deny>
      <ef:actor id=”actor_id”>
        <ef:action-list>
          <ef:read/>
          <ef:execute/>
          ...
        </ef:action-list>
      </ef:actor>
    </ef:acl-deny>
  </ef:acl>
...
```

The `id` attribute of an `ef:actor` can refer to a predefined `ef:acl-actor` or directly to an EnginFrame user ID\. 

There are four kinds of actions EnginFrame can accept\. The action meaning and the consequent EnginFrame behavior depends on the type of the resource that the ACL is applied to\. The four kinds of actions are the following:
+  `<ef:read/>` 
+  `<ef:write/>` 
+  `<ef:execute/>` 
+  `<ef:delete/>` 

Here an example of an ACL definition follows:

```
...
  <ef:acl-list>
    ...
    <ef:acl id="priv-exec">
      <ef:info>Privileged permissions for Admins</ef:info>
      <ef:acl-priority>deny</ef:acl-priority>
      <ef:acl-allow>
        <ef:actor id="efadmin">
          <ef:action-list>
            <ef:read/>
            <ef:write/>
            <ef:execute/>
            <ef:delete/>
          </ef:action-list>
        </ef:actor>
      </ef:acl-allow>
    </ef:acl>
    ...
  </ef:acl-list>
  ...
```

### Condition based ACL<a name="conditionBased-ACL"></a>

An ACL can include some extra conditions on granting access to a resource\. 

These conditions can take into account the value of session variables, system properties, and `xpath` expressions and be combined using the logical operators: `or`, `and`, `not`, and `equals`\. 

This is illustrated in the following example\.

```
...
<ef:acl-list>
   ...
  <ef:acl id="project-acme">
    <ef:info>
       Privileged permissions for Project ACME
    </ef:info>
    <ef:acl-priority>deny</ef:acl-priority>
    <ef:acl-allow>
       <ef:actor id="company-users">
         <ef:condition>
           <ef:or>
             <ef:and>
               <ef:equals type=”session”
                          id=”project”
                          value=”acme”
                          casesensitive=”true”/>
               <ef:equals type=”session”
                          id=”${project}_responsible”
                          value=”true”
                          casesensitive=”false”/>
             </ef:and>
             <ef:and>
               <ef:equals type=”session”
                          id=”administrator”
                          value=”true”
                          casesensitive=”false”/>
               <ef:not>
                 <ef:equals type=”property”
                            id=”${EF_USER}”
                            value=”jack”
                            casesensitive=”true”/>
               </ef:not>
             </ef:and>
           </ef:or>
         </ef:condition>
         <ef:action-list>
           <ef:read/>
           <ef:write/>
           <ef:execute/>
           <ef:delete/>
         </ef:action-list>
       </ef:actor>
    </ef:acl-allow>
  </ef:acl>
   ...
</ef:acl-list>
```

A user can access resources guarded by the "project\-acme" ACL only if one of the following conditions is true:
+  The user belongs to `"company-users"`, the session variable `"project"` is present and its value is `"acme"`, and the session variable `"acme_responsible"` is set to `"true"` independently from the case of letters\.
+  The session variable `"administrator"` is “true” independently from case of letters, and it isn't named `"jack"`\. 

The `ef:and` and `ef:or` tags are condition containers\. `ef:and` evaluates to true when all of the included conditions evaluate to true\. `ef:or` evaluates to true when at least one of its conditions evaluates to true\.

The `ef:not` might contain only one condition and it negates the result of its evaluation\. 

The `ef:equals` tag checks two arguments for equality\. The arguments to check are defined by the `type` and by the `id` attributes\. The `casesensitive` attribute specifies if the letter case matching is taken into account\. 

The `type` can refer to three different kinds of values:

Session variables  
The value to be checked is a session variable with the specified `id`\.   
The following is the session variable from the preceding example\.  

```
<ef:equals type=”session”
          id=”administrator”
          value=”true”
          casesensitive=”false”/>
```
EnginFrame checks if a session variable named `administrator` is defined and its value is `true`\. 

System properties  
The value to be checked is a system property with the specified `id`\. EnginFrame system properties are loaded by the JVM, passed to the JVM using the command line \(for example, –Dname=value\), and loaded from the EnginFrame configuration files\.   

```
<ef:equals type=”property”
          id=”${EF_USER}”
          value=”mary”
          casesensitive=”true”/>
```
EnginFrame checks if the system property named `${EF_USER}` has the value `mary`\.

XPath expressions  
The value to be checked is the one extracted from the current DOM by the XPath expression specified in the `id` attribute\.   

```
<ef:equals type=”xpath”
          id=”starts-with(//ef:profile/ef:user/., ‘br’)”
          value=”true”
          casesensitive=”true”/>
```
EnginFrame checks if the HTML DOM element `//ef:profile/ef:user/text()` starts with `br`\.