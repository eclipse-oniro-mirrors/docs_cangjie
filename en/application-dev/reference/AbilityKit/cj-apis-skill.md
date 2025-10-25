# ohos.skill

This module introduces the skill tag object.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class Skill

```cangjie
public class Skill {
    public let actions: Array<String>
    public let entities: Array<String>
    public let uris: Array<SkillUri>
    public let domainVerify: Bool
}
```

**Description:** The skill tag object. Third-party applications can obtain skill information via [getBundleInfoForSelf](./cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32), where the input parameter bundleFlags must include at least GET_BUNDLE_INFO_WITH_HAP_MODULE, GET_BUNDLE_INFO_WITH_ABILITY, and GET_BUNDLE_INFO_WITH_SKILL.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let actions

```cangjie
public let actions: Array<String>
```

**Description:** The collection of Actions received by the Skill.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let domainVerify

```cangjie
public let domainVerify: Bool
```

**Description:** The DomainVerify value received by the Skill, only existing in AbilityInfo.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let entities

```cangjie
public let entities: Array<String>
```

**Description:** The collection of Entities received by the Skill.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let uris

```cangjie
public let uris: Array<SkillUri>
```

**Description:** The collection of URIs for Want matching.

**Type:** Array\<[SkillUri](#class-skilluri)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## class SkillUri

```cangjie
public class SkillUri {
    public let scheme: String
    public let host: String
    public let port: Int32
    public let path: String
    public let pathStartWith: String
    public let pathRegex: String
    public let uriType: String
    public let utd: String
    public let maxFileSupported: Int32
    public let linkFeature: String
}
```

**Description:** Describes URI identification information.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let host

```cangjie
public let host: String
```

**Description:** Identifies the host address portion of the URI, meaningful only when scheme exists.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let linkFeature

```cangjie
public let linkFeature: String
```

**Description:** Identifies the feature type provided by the URI, used for implementing inter-application jumps, only existing in AbilityInfo.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let maxFileSupported

```cangjie
public let maxFileSupported: Int32
```

**Description:** For specified file types, identifies the maximum number that can be received or opened at once.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let path

```cangjie
public let path: String
```

**Description:** Identifies the path portion of the URI, meaningful only when both scheme and host exist.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let pathRegex

```cangjie
public let pathRegex: String
```

**Description:** Identifies the path portion of the URI for regular expression matching, meaningful only when both scheme and host exist.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let pathStartWith

```cangjie
public let pathStartWith: String
```

**Description:** Identifies the path portion of the URI for prefix matching, meaningful only when both scheme and host exist.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let port

```cangjie
public let port: Int32
```

**Description:** Identifies the port portion of the URI, meaningful only when both scheme and host exist.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let scheme

```cangjie
public let scheme: String
```

**Description:** Identifies the protocol name of the URI, common examples include http, https, file, ftp, etc.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let uriType

```cangjie
public let uriType: String
```

**Description:** Identifies the data type matching the Want, using MIME (Multipurpose Internet Mail Extensions) type specifications.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let utd

```cangjie
public let utd: String
```

**Description:** Identifies the standardized data type of the URI matching the Want, applicable for scenarios like sharing.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21