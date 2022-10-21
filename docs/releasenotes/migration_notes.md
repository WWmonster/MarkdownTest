Migration Notes
---------------

5.19.0
------

### Rule Services

Default OpenL properties are initialized in PropertySourcesLoader now. Add the following lines into web.xml:  
`<context-param>   <description>Load default and application properties to the Spring application   environment.</description>   <param-name>contextInitializerClasses</param-name>   <param-value>org.openl.spring.env.PropertySourcesLoader</param-value>   </context-param>` All OpenL-related properties should be in a single file. Merge rules-production.properties , ruleservice-ext.properties , openl-ruleservice.properties into application.properties. It is also recommended to remove default properties from the merged file.

### OpenL Maven Plugin

JavaWrapperAntTask was replaced with openl-maven-plugin. Use ['generate'](files/openl-tablets/5.19.0/OpenL Tablets - Maven Plugin Guide/generate-mojo.html) goal to generate Java beans from OpenL datatypes

The following properties were changed

Before

After

ruleservice.openl.home

openl.home

ruleservice.datasource.repositoryPropertiesFile = rules-production.properties

Removed.

production-repository.factory = org.openl.rules.repository.factories.JdbcDBRepositoryFactory

production-repository.factory = org.openl.rules.repository.db.JdbcDBRepositoryFactory

### Core

*   OpenL does not use JCL loging framework anymore, all dependencies on JCL were removed. Use JSF4J instead.
*   RulesEngineFactory(File) was deprecated. Use RulesEngineFactory(URL) or RulesEngineFactory(String) instead  
    `String xlsxPath = "filepath/or/classpath/to/file.xlsx";      // The argument is a filepath. It is useful for JUnit tests   new RulesEngineFactory(xlsxPath);      //Alternative way, using a classpath   URL xlsxUrl = getClass().getResource(xlsxPath);   new RulesEngineFactory(xlsxUrl);`

### OpenL Rules

*   Add ‘rules.xml’ file to any rules projects which were based on a deprecated Eclipse rules project template
*   If the rules relied on ‘autoType’ property being off by default it is advised to check if rules are working correctly and add this property if necessary
*   It is also recommended to remove the following imports in 'Environment' table from the rules:
    *   import java.utils.Arrays
    *   import org.apache.commons.lang
    *   import org.dozer.mapping  
        OpenL has own 'smart' functions like isEmpty() and addAll()

5.19.5
------

### OpenL Rules

Used more accurate conversion from Double to BigDecimal type. Double (1.1) will be converted to BigDecimal(1.1) instead of BigDecimal(1.100000000000000088817841970012523233890533447265625)

5.19.6
------

### Core

Removed deprecated **IVocabulary** class

5.20.0
------

### Rules Service

The following properties were changed

Before

After

version-in-deployment-name = true

version-in-deployment-name = false

Changed behavior of the Deployment Repository because of the performance issue. In exceptional case it can be restored old behavior using **version-in-deployment-name=true**.

### Core

Java 7 is used as minimal supported version (Java 9 is now supported). Added validation of duplicated packages/classes inside OpenL WARs.

### OpenL Rules

The implicit casting from Double to Integer was removed as error-prone. So use a correct argument type or use round function.

5.21.0
------

### Rules Service

The following properties were changed

Before

After

repository.encode.decode.key = This is the key for password secure

repository.encode.decode.key =

### OpenL Rules

*   All rules calculations should be revised. Because of changed type of division operations, please be aware that 7/4 is equal 1.75, not 1. Returned type became Double instead of Integer. Users who still need to use whole number division logic will need to adjust their rules.
*   Because of more strict table structures, it is possible that some tables would not be compiled/parsed. In this case, please check neighboring rows/columns. All comments (notes) in cells must be started from '//' (two slashes)

5.21.1
------

### Rule Services

Switched to slf4j adapter in CXF library instead of direct usage of log4j

Deleted deprecated **org.openl.rules.ruleservice.publish.WebServicesRuleServicePublisher**

5.21.2
------

### Rule Services

Because of strict SOAP v1.1 validation, please be attentively that **null** values are sent like <aField xsi:nil="true" />

### OpenL Demo

All examples have been converted to XLSX format

5.21.3
------

### Rule Services

**<detail>** element was changed in SOAP fault message. **<type>** and **<stackTrace>** elements were added with additional description of the fault

### OpenL Rules

**@VariationsFromRules** annotation and **VariationDescription** class were deprecated. Please, remove reference on this classes, which will be deleted in OpenL Tablets v5.22.0

5.21.4
------

### OpenL Rules

Test tables don't support business dimensional properties, so replace all definition with \_context\_ input parameter

Expectations should be defined properly: only one result or error should be set in a test table, not both.

5.21.7
------

### Rules Service

The following properties were changed

Before

After

ruleservice.useRuleServiceRuntimeContext

Removed.

ruleservice.datasource.type = local

production-repository.factory = org.openl.rules.repository.LocalRepositoryFactory

ruleservice.datasource.type

Removed.

### OpenL Rules

*   Remove any references on **useRuleServiceRuntimeContext** in rules-deploy.xml files.
*   The following properties are removed:Custom1, Custom2 and Transactional.
*   Remove coma from lob name for backward compatibility
*   Map<String, String> will not be compiled (generic types are not supported by OpenL)
*   Generated getters and setters are compatible with JavaBean specs v1.01 now. So for fields like iCoin - getiCoin()/setiCoin() methods will be generated.

5.21.11
-------

### WebStudio

Old modeshape-based repositories are not supported, and all related libraries were removed from WebStudio

5.21.13
-------

### OpenL Rules

CalculationStep.getStepName() returns a value without type definition now. Was: "MyStep:Double". Became: "MyStep"

5.22.0
------

### OpenL Maven Plugin

Delete deprecated: generateUnitTests, unitTestTemplatePath, overwriteUnitTests in OpenL Maven Plugin

### OpenL Rules

*   Delete deprecated: org.openl.rules.calculation.result.convertor.\* org.openl.rules.calc.result.convertor.\*
*   Cells calculation order in Spreadsheet type table with non-spreadsheetresult return value is changed. Calculation of such spreadsheets may need to be updated or property "calculateAllCells = false" can be added for backward compatibility.
*   Month numbers are from 1 to 12 (January number is 1). Previously it was from 0.

5.22.2
------

### OpenL Rules

Behavior is changed for nulls for multiplication and division operation. For old behavior use **import org.openl.rules.binding.MulDivNullToOneOperators.\***

5.23.0
------

### WebStudio

All OpenL WebStudio related properties should be composed into a single file. Merge rules-production.properties , db.properties , system.properties into application.properties or webstudio.properties. It is also recommended to remove default properties from the merged file.

The following location can be used to store properties (the next overrides previous):

*   ${ user.dir}\\application.properties (RO)
*   ${ user.home}\\application.properties (RO)
*   ${ openl.home}\\{ appName}.properties (RW)

Where { appName} - is [Spring application name](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationContext.html#getApplicationName--) ([Servlet context path](https://docs.oracle.com/javaee/7/api/javax/servlet/ServletContext.html#getContextPath--)).

So for the simplest case, when **webstudio.war** is deployed in Tomcat, the appName is **webstudio** and file is **webstudio.properties**.

It allows to separate configs for different OpenL applications under the same server.  
Common settings also can be located in application.properties file.

The following properties were changed

Before

After

repository.encode.decode.key=This is the key for password secure

secret.key=

user.settings.home

Removed. **${ webstudio.home}/user-settings** directory can be deleted.

webstudio.home

openl.home

**design-repository**.\*\*\*\*\*

**repository.design**.\*\*\*\*\*

**production-repository**.\*\*\*\*\*

**repository.production**.\*\*\*\*\*

design-repository.factory = org.openl.rules.repository.factories.LocalJackrabbitRepositoryFactory

repository.design.factory=org.openl.rules.repository.git.GitRepository

org.openl.rules.repository.factories. LocalJackrabbitRepositoryFactory

Removed.

org.openl.rules.repository.factories. WebDavRepositoryFactory

Removed.

org.openl.rules.repository.factories. RmiJackrabbitRepositoryFactory

Removed.

Note 1: Supporting of the following Design & Deployment repositories were discontinued:

*   Remote RMI
*   Remote WebDav
*   Local (were replaced with GIT)

Use Migration Tool to convert them into DB or GIT based repositories if needed.

Note 2: **secret.key** property allows OpenL WebStudio to encode any properties ended with \*\*\*\***.pasword**. By default **secret.key** is empty that means all passwords are stored in the plain view. Decoding of the passwords happens only when two things are: **secret.key** is set and password is wrapped into ENC( eNcoDedPa$$w0RD ) signature. So there is possibbility to define as encodded password in properties files so and plain view password, when **secret.key** is set.

Before

After

repository.encode.decode.key=My $eCr3T  
design-repository.password=eNcoDedPa$$w0RD

secret.key=My $eCr3T  
repository.design.password=ENC(eNcoDedPa$$w0RD)  
  
Or:  
secret.key=My $eCr3T  
repository.design.password=plain PASSWORD

### Rules Services

The following properties were changed

Before

After

ruleservice.logging.store.enabled

ruleservice.store.logs.enabled

repository.encode.decode.key

secret.key

ruleservice.logging.store.cassandra.enabled

ruleservice.store.logs.cassandra.enabled

ruleservice.logging.store.type.cassandra.protocol.version

cassandra.protocol.version

ruleservice.logging.store.type.cassandra.schema.create

cassandra.schema.create

ruleservice.logging.store.elastic.enabled

ruleservice.store.logs.elasticsearch.enabled

The following deprecated properties files were deleted:

*   rules-production.properties
*   openl-ruleservice.properties
*   \*-ruleservice-ext.properties

The following properties files should be used:

*   application.properties
*   application-default.properties

### OpenL Rules

rules-deploy.xml should contain a correct set of actual publishers or publishers tag should be absent otherwise the project will not be deployed

5.23.1
------

### WebStudio

The following properties were changed

Before

After

default.openl.compatibility.version

openl.compatibility.version

Undefined.

webstudio.configured=false

### Rules Services

The following properties were changed

Before

After

ruleservice.baseAddress

Removed.

ruleservice.jackson.serializationInclusion = ALWAYS

ruleservice.jackson.serializationInclusion = USE\_DEFAULTS

5.23.3
------

### WebStudio

The setting "Unlimited numbers of copies" will automatically be set to false after migration to this version, and the setting "The maximum count of saved changes for each project:"=100 will be applied. If there is a need to store unlimited amount of changes, set the setting "Unlimited numbers of copies" = true before opening any project. This setting is changed to prevent uncontrolled consumption of free space on HDD/SDD for 'undo' operations during editing a project.

The following properties were changed

Before

After

project.history.count=0

project.history.count=100

project.history.unlimited=true

Removed. Use **project.history.count=**

### Rules Service

The following properties were changed

Before

After

ruleservice.aegisbinding.readXsiTypes

ruleservice.aegis.readXsiTypes

ruleservice.aegisbinding.writeXsiTypes

ruleservice.aegis.writeXsiTypes

ruleservice.aegisbinding.ignoreNamespaces

ruleservice.aegis.ignoreNamespaces

ruleservice.deployer.enable

ruleservice.deployer.enabled

DISABLED, ENABLED and SMART in ruleservice.jackson.defaultTypingMode

JAVA\_LANG\_OBJECT, OBJECT\_AND\_NON\_CONCRETE, NON\_CONCRETE\_AND\_ARRAYS, NON\_FINAL, EVERYTHING, DISABLED. [See ObjectMapper](http://fasterxml.github.io/jackson-databind/javadoc/2.10/com/fasterxml/jackson/databind/ObjectMapper.DefaultTyping.html)

ruleservice.jackson.defaultTypingMode = SMART

ruleservice.jackson.defaultTypingMode = JAVA\_LANG\_OBJECT

5.23.6
------

### WebStudio & Rule Services

The following properties were changed

Before

After

version-in-deployment-name

Removed.

5.23.8
------

### Rule Services

The following properties were changed

Before

After

ruleservice.datasource.filesystem.supportVersion

Removed.

ruleservice.datasource.deploy.clean.datasource

Removed. Use your startup script if it is required to clean files before run RuleServices.

ruleservice.datasource.dir

production-repository.uri

ruleservice.tmp.dir

Removed. **java.io.tmpdir** is used instead.

### OpenL Rules

The following API was deprecated

Before

After

org.openl.rules.ruleservice.core.interceptors. AnyType

org.openl.rules.ruleservice.core.interceptors. RulesType

org.openl.rules.project.resolving. CWPropertyFileNameProcessor

Remove any references from rules.xml files. The default implementation covers this functionality out-of-the-box.

org.openl.rules.project.resolving. PropertiesFileNameProcessor

Migrate custom implementation to use new API. Be noted that the default implementation covers multiple scenarios of parsing file names and can be used instead of the custom implementation.

5.23.9
------

### WebStudio

The following properties were changed

Before

After

**{ 0} { 1} { 2}** in repository.design.new-branch-pattern

**{ project-name} { username} { current-date}**

repository.design.new-branch**\-**pattern

repository.design.new-branch**.**pattern

repository.design.comment-validation-pattern

repository.design**.comment-template**.comment-validation-pattern

repository.design.invalid-comment-message

repository.design**.comment-template**.invalid-comment-message

repository.deploy-config.comment-validation-pattern

repository.deploy-config**.comment-template**.comment-validation-pattern

repository.deploy-config.invalid-comment-message

repository.deploy-config**.comment-template**.invalid-comment-message

repository.design.factory = org.openl.rules.repository.git.GitRepository

repository.design.factory = repo-git

repository.production.factory = org.openl.rules.repository.db.JdbcDBRepositoryFactory

repository.production.factory = repo-jdbc

org.openl.rules.repository.db.JdbcDBRepositoryFactory

repo-jdbc

org.openl.rules.repository.db.DatasourceDBRepositoryFactory

repo-jndi

org.openl.rules.repository.aws.S3Repository

repo-aws-s3

org.openl.rules.repository.git.GitRepository

repo-git

### Rules Services

Before

After

production-repository.factory = org.openl.rules.repository.LocalRepositoryFactory

production-repository.factory = repo-file

org.openl.rules.repository.db.JdbcDBRepositoryFactory

repo-jdbc

org.openl.rules.repository.db.DatasourceDBRepositoryFactory

repo-jndi

org.openl.rules.repository.aws.S3Repository

repo-aws-s3

org.openl.rules.repository.git.GitRepository

repo-git

ruleservice.datasource.filesystem.supportDeployments

production-repository.support-deployments

5.24.0
------

### WebStudio

*   Project changes history created before migrating to 5.24.0 is not available after migration. The files will remain in the folder but in WebStudio there will be no records in "Local Changes" and no possibility to restore them. A user must save the necessary changes before the migration.
*   While migrating from 5.23.x to 5.24.0, all necessary files and properties are moved automatically. To migrate from earlier versions, such as 5.21.16 or 5.22.7, migrate manually to the last minor version of 5.23.x and then to 5.24.0. That is, perform migration step by step, for example, 5.22.7 > 5.23.11 > 5.24.0. More details are in the document [Migration from earlier than 5.23.x](uploads/Migration%20from%20earlier%20than%205.23.x.pdf).
*   Default repository folders are changed in 5.24.0. New folder paths are used by default only for a freshly installed 5.24.0. After migration from 5.23.x, old local paths remain, and if adding new repositories in 5.24.0, the path is generated from the old path.
*   The administrator user is deleted after migration to 5.24.0. To set a new administrator user, use the "security.administrators" property in the webstudio.properties file.

### Rule Services

The following properties were changed

Before

After

ruleservice.datasource.filesystem.supportDeployments

Removed.

production-repository.support-deployments

Removed.

ruleservice.instantiation.strategy.lazy=true

ruleservice.instantiation.strategy.lazy=false

5.25.3 (for 5.26.0)
-------------------

### Core:

**DoubleValue** and similar types in the **org.openl.meta package** are deprecated for usage. It should be replaced by similar types from the Java language, E.g. **DoubleValue** to **Double**, **BigIntegerValue** to **BigInteger** and so on

To prevent the compilation errors in 5.26.0, the \*Value-specific operation should be replaced. See proposed fixes below (Compatible with 5.24.0):

\*Value-specific operation

Proposed fix

Alternative fix

cast(a, 1)

(Integer) a

DoubleValue.round(a , n)

round( a , n )

(DoubleValue) round( a, n )

a.getValue()

(Double) a

DoubleValue.add(a, b)

a + b

(DoubleValue) ( a + b )

a.length

length( a )

(int) (cast((a),1))

(Integer) a

isNumeric(str)

like( str, "#+" )  
like( str, "####" )

isNotEmpty( toInteger( str ) )  
isNotEmpty( toDouble( str ) )

SOAP/WSDL services and Aegis converters are deprecated for usage. It should be migrated to REST/OpenAPIv3 services.

5.26.0
------

### Security

*   If the SSO:SAML user mode was used in 5.25, for successful migration to 5.26, add the "Entity ID" parameter to webstudio.properties (entity ID = Client saml name) before the migration. Example: **security.saml.entity-id=webstudio**. This parameter can also be added in the "Entity ID" field in the installation wizard/Step3. Note that in 5.25, if the entity ID is not provided, the default value "http://localhost:8080/webstudio/saml/metadata" is used by the system. In 5.26, the default value is "webstudio".  
    The link for downloading WebStudio SAML metadada XML is http://localhost:8080/webstudio/saml2/service-provider-metadata/webstudio .  
    Note that a private certificate is now generating per WebStudio instance and stores in the properties file. Previous hardcoded private key was removed from the Java KeyStore. It means, that public key for the IdP must be updated from the WebStudio SAML metadata XML.

### Webstudio, Rule Services

*   Java 8 is not supported any more.
*   Due to **MSSQL driver** upgrade, use **encrypt=false;trustServerCertificate=true**; in the connection string if your server does not support encryption. For more information, see:  
    [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/ssl-certificate-rotation-sqlserver.html](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/ssl-certificate-rotation-sqlserver.html) and  
    [https://docs.microsoft.com/en-us/sql/connect/jdbc/release-notes-for-the-jdbc-driver?view=sql-server-ver15#changes-in-102](https://docs.microsoft.com/en-us/sql/connect/jdbc/release-notes-for-the-jdbc-driver?view=sql-server-ver15#changes-in-102)
*   Upgrading **H2 DB** requires migrate according to the migration guide are described in [https://www.h2database.com/html/migration-to-v2.html](https://www.h2database.com/html/migration-to-v2.html)
*   Starting from OpenL Tablets 5.26.0, Groovy Scripts have an access to all Java types of a project and its dependency projects generated from their Datatype tables. It was the most requested feature after Groovy Scripts support had been introduced. To support the feature we had to change a module compilation algorithm to use the same classloader for each project. Before the change, each module in the project had used its own classloader. The change may break backward compatibility **if multiple projects use Datatypes with the same name** even if the modules don’t have a relationship, but a relationship between projects exists. To migrate your projects in this case, you should define unique package names there (refer to Ref Guide, Dev Properties - > Dev Properties List section).
