# JFrog MCP Server Tools

This is the complete reference of tools exposed by the JFrog Platform MCP Server,
grouped by product and domain.

> The JFrog MCP Server is a **remote** server hosted on JFrog Cloud. Its tool set
> is updated server-side, so you automatically get new tools and improvements as
> they are released — no client upgrade required.

## Available Toolsets

| Toolset                                                   | Description                                                               |
| --------------------------------------------------------- | ------------------------------------------------------------------------- |
| [Access: Tokens](#access-tokens)                          | Access token creation, listing, and revocation                            |
| [Access: OIDC](#access-oidc)                              | OpenID Connect identity provider configuration                            |
| [Access: Projects](#access-projects)                      | Project lifecycle, membership, roles, and repository assignment           |
| [Access: Roles](#access-roles)                            | Global role creation and management                                       |
| [Access: Stages](#access-stages)                          | Platform stages discovery                                                  |
| [Access: Users and Groups](#access-users-and-groups)      | Platform user and group listing and lookup                                 |
| [Artifactory: Repositories](#artifactory-repositories)    | Repository creation, listing, and update                                  |
| [Artifactory: Packages](#artifactory-packages)            | Package version queries, locations, and install commands                  |
| [Artifactory: Builds](#artifactory-builds)                | Build discovery, run history, and build info retrieval                    |
| [Artifactory: Federation](#artifactory-federation)        | Federated repository health, conflicts, and configuration synchronization |
| [Artifactory: Storage](#artifactory-storage)              | Artifact and folder storage metadata, listing, and permissions            |
| [Security](#security)                                     | Catalog vulnerabilities and Xray artifact summaries                       |
| [Curation](#curation)                                     | Package compliance, audit events, and waiver requests                    |
| [Distribution](#distribution)                             | Release bundle distribution, tracking, signing keys, and edge management |
| [Workers](#workers)                                       | JFrog Workers listing, creation, update, retrieval, and execution history |
| [Event](#event)                                           | Webhook domain catalog and subscription management                        |
| [Evidence: Config](#evidence-config)                      | Evidence service configuration and category administration                |
| [Evidence: Categories](#evidence-categories)              | Evidence category discovery                                               |
| [Evidence: Records](#evidence-records)                    | Evidence record search, retrieval, creation, and rendering                |
| [JFrog AppTrust](#jfrog-apptrust)                         | Application lifecycle, versioning, promotion, and release management      |

---

<a id="access-tokens" name="access-tokens"></a>
<details>
<summary><b>Access: Tokens</b></summary>

### `access_tokens_create`

*Note: The name of this tool will change in an upcoming release.*

Create a new access token.

**Parameters**:

* `grant_type`: `client_credentials` for new tokens, `refresh_token` to refresh (string, optional)
* `refresh_token`: Refresh token value; required when grant\_type is `refresh_token` (string, optional)
* `username`: Username to create the token for (string, optional)
* `scope`: Scope of access. Default: `applied-permissions/user` (string, optional)
* `expires_in`: Token expiry in seconds; 0 for non-expirable (admin only) (integer, optional)
* `refreshable`: Whether the token can be refreshed (boolean, optional)
* `audience`: Space-separated service IDs that should accept this token (string, optional)
* `description`: Human-readable token description (string, optional)
* `include_reference_token`: Generate a reference token in addition to the full token (boolean, optional)
* `force_revocable`: Make the token explicitly revocable (boolean, optional)
* `project_key`: Scope the token to a specific project (string, optional)

### `access_tokens_list`

List access tokens with filters.

**Parameters**:

* `username`: Filter tokens by username (string, optional)
* `description`: Filter tokens by description (partial match) (string, optional)
* `token_id`: Filter by a specific token ID (string, optional)
* `refreshable`: Filter by refreshable status (boolean, optional)
* `order_by`: Sort field — `created`, `expiry`, or `subject` (string, optional)
* `descending_order`: Sort in descending order (boolean, optional)

### `access_tokens_revoke`

Revoke an existing access token.

**Parameters**:

* `token`: The token value to revoke (JWT or reference token) (string, required)

</details>

<a id="access-oidc" name="access-oidc"></a>
<details>
<summary><b>Access: OIDC</b></summary>

### `access_oidc_create_configuration`

Create a new OIDC identity provider configuration.

**Parameters**:

* `name`: Unique name for the OIDC configuration (string, required)
* `issuer_url`: The OIDC issuer URL (string, required)
* `audience`: Expected audience claim in the ID token (string, optional)
* `description`: Human-readable description (string, optional)
* `provider_type`: Identity provider type — `generic`, `GitHub`, or `Azure` (string, optional)
* `token_issuer`: Token issuer identifier for claim validation (string, optional)
* `enable_permissive_configuration`: Allow permissive OIDC validation (boolean, optional)
* `use_default_proxy`: Route discovery requests through the default HTTP proxy (boolean, optional)
* `azure_app_id`: Azure Application ID; required when provider\_type is `Azure` (string, optional)

</details>

<a id="access-projects" name="access-projects"></a>
<details>
<summary><b>Access: Projects</b></summary>

### `access_projects_create`

*Replaces `create_project`.*

Create a new Access project.

**Parameters**:

* `project_key`: Unique project identifier (string, required)
* `display_name`: Human-readable project name (string, required)
* `description`: Project description (string, optional)
* `admin_privileges`: Admin privilege settings — manage\_members, manage\_resources, manage\_security\_assets, index\_resources, allow\_ignore\_rules (object, optional)
* `storage_quota_bytes`: Storage quota in bytes (integer, optional)

### `access_projects_get`

*Replaces `get_project_info`.*

Get Access project details.

**Parameters**:

* `project_key`: The unique project key to look up (string, required)

### `access_projects_update`

Update an Access project.

**Parameters**:

* `project_key`: The project key to update (string, required)
* `display_name`: New display name (string, optional)
* `description`: New description (string, optional)
* `admin_privileges`: Updated admin privileges (object, optional)
* `storage_quota_bytes`: New storage quota in bytes (integer, optional)

### `access_projects_create_role`

Create a custom project role.

**Parameters**:

* `project_key`: The project key (string, required)
* `name`: Unique role name within the project (string, required)
* `type`: Role type — `CUSTOM` or `PREDEFINED` (string, required)
* `description`: Role description (string, optional)
* `environments`: Environments this role applies to, e.g. `["DEV", "PROD"]` (string\[], optional)
* `actions`: Allowed actions, e.g. `["READ_REPOSITORY", "DEPLOY_BUILD"]` (string\[], optional)

### `access_projects_update_role`

Update a project role.

**Parameters**:

* `project_key`: The project key (string, required)
* `role_name`: The name of the role to update (string, required)
* `type`: Role type — only `CUSTOM` roles can be updated (string, required)
* `description`: Updated role description (string, optional)
* `environments`: Updated environments list (string\[], optional)
* `actions`: Updated actions list (string\[], optional)

### `access_projects_get_user`

Get user membership in a project.

**Parameters**:

* `project_key`: The project key (string, required)
* `user`: The username to look up (string, required)

### `access_projects_upsert_user`

Add or update user in a project.

**Parameters**:

* `project_key`: The project key (string, required)
* `user`: The username to add or update (string, required)
* `roles`: Role names to assign — replaces all existing roles (string\[], required)

### `access_projects_list_groups`

List groups assigned to a project.

**Parameters**:

* `project_key`: The project key (string, required)

### `access_projects_upsert_group`

Add or update group in a project.

**Parameters**:

* `project_key`: The project key (string, required)
* `group`: The group name (string, required)
* `roles`: Role names to assign — replaces all existing roles (string\[], required)

### `access_projects_get_repository`

Get repository project status.

**Parameters**:

* `repo_name`: The repository name to look up (string, required)

### `access_projects_move_repository_to_project`

Move a repository to a project.

**Parameters**:

* `repo_name`: The repository name to move (string, required)
* `target_project_key`: The project key to move the repository into (string, required)
* `force`: Force the move even if validation checks fail (boolean, optional)

### `access_projects_share_repository_with_all`

Share repository with all projects.

**Parameters**:

* `repo_name`: The repository name to share (string, required)
* `read_only`: Restrict sharing to read-only access (boolean, optional)

### `access_projects_list`

*Replaces `list_projects`.*

List all JFrog projects.

**Parameters**:

* No parameters required

</details>

<a id="access-roles" name="access-roles"></a>
<details>
<summary><b>Access: Roles</b></summary>

### `access_roles_create_global_role`

*Available from Access - 7.77.*

Create a custom global role with platform-wide permissions.

**Parameters**:

* `name`: Unique name for the new global role (string, required)
* `type`: Role type — must be `CUSTOM_GLOBAL` (string, required)
* `environments`: Stage names this role applies to, e.g. `["DEV", "STAGING", "PROD"]` (string\[], required)
* `actions`: Permitted actions, e.g. `["READ_REPOSITORY", "DEPLOY_CACHE_REPOSITORY"]` (string\[], required)
* `description`: Role description (string, optional)

### `access_roles_update_global_role`

*Available from Access - 7.77.*

Update an existing custom global role.

**Parameters**:

* `role_name`: Name of the existing global role to update (string, required)
* `description`: Updated role description (string, optional)
* `environments`: Updated stage names list (string\[], optional)
* `actions`: Updated permitted actions list (string\[], optional)

</details>

<a id="access-stages" name="access-stages"></a>
<details>
<summary><b>Access: Stages</b></summary>

### `access_stages_list_global_stages`

*Replaces `get_jfrog_global_environments`.*

*Available from Access - 7.125.3.*

List all global stages configured in the platform.

**Parameters**:

* `project_key`: Filter stages by project key (string, optional)
* `scope`: Filter by scope — `global` or `project` (string, optional)
* `category`: Filter by stage category — `none`, `code`, `promote`, or `release` (string, optional)

</details>

<a id="access-users-and-groups" name="access-users-and-groups"></a>
<details>
<summary><b>Access: Users and Groups</b></summary>

### `access_users_list`

List users in the JFrog platform.

**Parameters**:

* `status`: Filter by account status — `invited`, `enabled`, `disabled`, or `locked` (string, optional)
* `username`: Filter by username (contains match) (string, optional)
* `only_admins`: Filter to admin users only; cannot be combined with `project_key` (boolean, optional)
* `project_key`: Filter users within a project context; cannot be combined with `only_admins` (string, optional)
* `limit`: Maximum number of users to return; default 1000 (integer, optional)
* `cursor`: Pagination cursor from a prior response (string, optional)

### `access_users_get`

Get details of a specific user by username.

**Parameters**:

* `username`: Username to look up (string, required)

### `access_groups_list`

List all groups in the JFrog platform.

**Parameters**:

* `group_name`: Filter by group name pattern (string, optional)
* `project_key`: Filter groups by project key (string, optional)
* `limit`: Maximum number of groups to return; default 1000 (integer, optional)
* `cursor`: Pagination cursor from a prior response (string, optional)
* `descending_order`: Return groups in descending lexical order (boolean, optional)

### `access_groups_get`

Get details of a specific group by name.

**Parameters**:

* `group_name`: Group name to look up (string, required)

</details>

<a id="artifactory-repositories" name="artifactory-repositories"></a>
<details>
<summary><b>Artifactory: Repositories</b></summary>

### `artifactory_repositories_create`

*Replaces `create_repository`.*

Create a new Artifactory repository.

**Parameters**:

* `repo_key`: Unique repository key (string, required)
* `rclass`: Repository class — local, remote, virtual, or federated (string, required)
* `packageType`: Package type for the repository (string, required)
* `description`: Repository description (string, optional)
* `url`: Upstream URL for remote repositories (string, optional)
* `repoLayoutRef`: Repository layout key (string, optional)
* `handleReleases`: Whether the repository handles release artifacts (boolean, optional)
* `handleSnapshots`: Whether the repository handles snapshot artifacts (boolean, optional)
* `xrayIndex`: Enable Xray indexing for this repository (boolean, optional)
* `contentSynchronisation`: Smart Remote Repository synchronization settings (object, optional)
* `cdnRedirect`: Enable CDN Distribution for this repository (boolean, optional)
* `repositories`: Repository keys to include in a virtual repository (string\[], optional)
* `defaultDeploymentRepo`: Default deployment repository for a virtual repository (string, optional)
* `projectKey`: Project key to assign this repository to (string, optional)
* `environments`: Environments to assign to the repository (string\[], optional)

### `artifactory_repositories_get`

Retrieve the configuration of a single Artifactory repository by key.

**Parameters**:

* `repo_key`: Repository key to look up (string, required)

### `artifactory_repositories_list`

*Replaces `list_repositories`.*

List JFrog repositories.

**Parameters**:

* `type`: Filter by repository type (string, optional)
* `packageType`: Filter by package type (string, optional)
* `project`: Filter by project key (string, optional)

### `artifactory_repositories_update`

Update the configuration of an existing Artifactory repository.

**Parameters**:

* `repo_key`: Repository key to update (string, required)
* `description`: New repository description (string, optional)
* `notes`: Free-text notes about the repository (string, optional)
* `includesPattern`: Artifact inclusion pattern (string, optional)
* `excludesPattern`: Artifact exclusion pattern (string, optional)
* `repoLayoutRef`: Repository layout key (string, optional)
* `handleReleases`: Whether this repository handles release artifacts (boolean, optional)
* `handleSnapshots`: Whether this repository handles snapshot artifacts (boolean, optional)
* `xrayIndex`: Enable or disable Xray indexing (boolean, optional)
* `propertySets`: Property set names to assign (string\[], optional)
* `url`: Upstream URL for remote repositories (string, optional)
* `projectKey`: Project key to assign this repository to (string, optional)
* `environments`: Environments to assign to the repository (string\[], optional)
* `repositories`: Repository keys to include in a virtual repository (string\[], optional)
* `defaultDeploymentRepo`: Default deployment repository for a virtual repository (string, optional)

</details>

<a id="artifactory-packages" name="artifactory-packages"></a>
<details>
<summary><b>Artifactory: Packages</b></summary>

### `artifactory_packages_get_versions`

*Replaces `get_rt_package_versions`.*

*Available from Artifactory - 7.146.0.*

List versions of a package stored in Artifactory with summary information.

**Parameters**:

* `package_name`: Package name to search for (string, required)
* `package_type`: Package type in lowercase (string, required)
* `max_results`: Maximum number of versions to return (integer, optional)
* `ignore_pre_release`: Exclude pre-release versions (boolean, optional)
* `order_by`: Sort field, e.g. `SEMVER`, `VERSION`, `MODIFIED`, or `STATS_DOWNLOAD_COUNT` (string, optional)
* `sort_direction`: Sort direction, e.g. `ASC` or `DESC` (string, optional)

### `artifactory_packages_get_version_repositories`

*Replaces `get_rt_package_version`.*

*Available from Artifactory - 7.146.0.*

Find which Artifactory repositories hold a specific package version.

**Parameters**:

* `package_name`: Package name (string, required)
* `package_type`: Package type in lowercase (string, required)
* `version`: Exact version string to look up (string, required)

### `artifactory_packages_get_install_instructions`

*Available from Artifactory - 7.133.3.*

Get native client commands for installing a specific package version.

**Parameters**:

* `package_name`: Package name (string, required)
* `package_type`: Package type in lowercase (string, required)
* `package_version`: Version string or tag (string, required)
* `leadfile_path`: Relative storage path of the leading file for this package version (string, required)
* `repo_key`: Repository key where the package resides (string, required)

</details>

<a id="artifactory-builds" name="artifactory-builds"></a>
<details>
<summary><b>Artifactory: Builds</b></summary>

### `artifactory_builds_list_builds`

*Available from Artifactory - 7.120.*

List Artifactory builds using AQL. Returns build names, numbers, and timestamps.

**Parameters**:

* `aql_query`: AQL query string for the builds domain. Must use `builds.find()`, include mandatory fields (`name`, `number`, `repo`), and include `.limit(N)` (string, required)

### `artifactory_builds_list_build_runs`

*Available from Artifactory - 7.120.*

List all runs of a named build. Returns run numbers and timestamps sorted newest first.

**Parameters**:

* `aql_query`: AQL query string filtered by build name. Must use `builds.find({"name":"<build-name>"})`, include mandatory fields (`name`, `number`, `repo`), and include `.limit(N)` (string, required)

### `artifactory_builds_get_info`

*Available from Artifactory - 7.120.*

Get the full build info for a specific build run. Returns build metadata, modules, artifacts, dependencies, and CI/VCS information.

**Parameters**:

* `build_name`: Build name (string, required)
* `build_number`: Build number (string, required)
* `started`: Build start timestamp for disambiguation (string, optional)
* `diff`: An older build number to diff against (string, optional)
* `project`: Project key the build belongs to (string, optional)

</details>

<a id="artifactory-federation" name="artifactory-federation"></a>
<details>
<summary><b>Artifactory: Federation</b></summary>

### `artifactory_federation_get_status`

Get federated repository health status.

**Parameters**:

* `status`: Comma-separated status filter, e.g. `HEALTHY,ERROR,DELAYED,NOT_AVAILABLE,PENDING_FS,FULL_SYNC_RUNNING,DISABLED` (string, optional)

### `artifactory_federation_get_conflicts`

Find federated repositories with configuration conflicts.

**Parameters**:

* No parameters required

### `artifactory_federation_update_repo_config`

Synchronize federated repository configuration to members.

**Parameters**:

* `repo_key`: Repository key of the federated repository to synchronize (string, required)

</details>

<a id="artifactory-storage" name="artifactory-storage"></a>
<details>
<summary><b>Artifactory: Storage</b></summary>

### `artifactory_storage_artifact_info`

*Available from Artifactory - 7.135.*

Retrieve storage information about a file or folder in an Artifactory repository.

**Parameters**:

* `repo_key`: Repository key (string, required)
* `item_path`: Path to the file or folder within the repository (string, required)
* `list`: Return a flat or deep folder listing instead of basic metadata (boolean, optional)
* `deep`: Recursive listing; only applies when `list` is true (boolean, optional)
* `depth`: Depth limit for deep listing; only applies when `list` and `deep` are true (integer, optional)
* `list_folders`: Include folders in listing results; only applies when `list` is true (boolean, optional)
* `md_timestamps`: Include metadata timestamps in listing output; only applies when `list` is true (boolean, optional)
* `include_root_path`: Include the folder root path in listing output; only applies when `list` is true (boolean, optional)
* `stats`: Return download statistics (boolean, optional)
* `last_modified`: Return the last-modified timestamp (boolean, optional)
* `properties`: Retrieve item properties; empty string returns all, or pass comma-separated keys (string, optional)
* `permissions`: Return access permission details for the item (boolean, optional)

</details>

<a id="security" name="security"></a>
<details>
<summary><b>Security</b></summary>

### `xray_artifact_get_summary`

*Replaces `artifactory_artifacts_get_summary`.*

Get the Xray security summary of one or more artifacts.

**Parameters**:

* `paths`: Artifact paths in Artifactory (string\[], optional)
* `checksums`: SHA-256 or SHA-1 checksums (string\[], optional)

### `xray_artifact_get_violations`

Get Xray policy violation counts for one artifact across one or more versions.

**Parameters**:

* `artifactory_id`: Xray Artifactory server ID for the artifact (string, required)
* `versions`: Artifact versions to inspect, each with `sha256` and `repo_paths` (object\[], required)
* `repository_type`: Repository package type, e.g. `Maven`, `Docker`, `npm`, or `Generic` (string, optional)
* `include_summary`: Include violation count summaries by category and severity (boolean, optional)
* `new_severities`: Use Critical/High/Medium/Low/Unknown severity names (boolean, optional)

### `xray_sbom_search_impacted_resources`

Search Xray impacted resources by vulnerability, package, package version, or SaaS service.

**Parameters**:

* `vulnerability`: CVE ID or Xray vulnerability ID to search for (string, optional)
* `package_name`: Package or component name to search for (string, optional)
* `package_type`: Package ecosystem/type for package searches (string, optional)
* `package_version`: Exact package version to search for (string, optional)
* `namespace`: Package namespace for package-version searches (string, optional)
* `ecosystem`: Package ecosystem value for package-version searches (string, optional)
* `service_name`: SaaS service name to search for (string, optional)
* `provider_name`: SaaS provider name for service searches (string, optional)
* `limit`: Maximum number of resources to return (integer, optional)
* `last_key`: Pagination cursor from a previous response (string, optional)

### `catalog_vulnerabilities_get`

*Replaces `list_catalog_vulnerabilities`.*

Get vulnerability information including affected packages and versions.

**Parameters**:

* `cve_id`: CVE identifier to query (string, required)

### `catalog_packages_versions_vulnerabilities`

*Replaces `list_catalog_version_vulnerabilities`.*

List known vulnerabilities for a specific package version.

**Parameters**:

* `package_type`: Package type (string, required)
* `package_name`: Package name (string, required)
* `package_version`: Package version (string, required)

### `catalog_packages_list_versions`

*Replaces `list_catalog_package_versions`.*

List versions of a publicly available package.

**Parameters**:

* `package_type`: Package type (string, required)
* `package_name`: Package name (string, required)
* `vulnerability_status`: Filter — `vulnerable`, `invulnerable`, or `any` (string, required)

### `catalog_packages_get`

*Replaces `get_catalog_package_entity`.*

Get public information about a software package.

**Parameters**:

* `package_type`: Package type (string, required)
* `package_name`: Package name (string, required)
* `package_version`: Version to query; default `latest` (string, optional)

</details>

<a id="curation" name="curation"></a>
<details>
<summary><b>Curation</b></summary>

### `jfs_curation_check_remote_package_compliance`

*Replaces `curation_packages_get_status`.*

*Available from Xray - 3.147.2.*

Check JFrog Curation compliance for a third-party package before installing or recommending it.

**Parameters**:

* `package_name`: Package name (string, required)
* `package_type`: Package manager type — `npm`, `pypi`, `maven`, `nuget`, or `gems` (string, required)
* `package_version`: Version to check (string, required)
* `remote_source_url`: Registry URL containing `/artifactory/` if configured; otherwise empty string (string, required)

### `jfs_curation_query_audit_events`

*Available from Xray - 3.112.0.*

Search blocked Curation package audit events. Covers policy blocks only — not approved, passed, or dry-run events.

**Parameters**:

* `package_type`: Package ecosystem — `npm`, `PyPI`, `Maven`, `Gradle`, `NuGet`, `Go`, and others (string, optional)
* `package_name`: Exact package name (string, optional)
* `package_version`: Exact package version (string, optional)
* `curated_repository_name`: Curated repository where the block occurred (string, optional)
* `created_at_start`: Event time lower bound, RFC3339 (string, optional)
* `created_at_end`: Event time upper bound, RFC3339 (string, optional)
* `num_of_rows`: Page size, 1–2000; default 1250 (integer, optional)
* `offset`: Pagination offset; use `meta.next_offset` from a prior response (integer, optional)
* `direction`: Sort direction — `asc` or `desc` (string, optional)
* `include_total`: Include `meta.total_count` in the response (boolean, optional)

### `jfs_curation_create_waiver_request`

*Available from Xray - 3.148.0.*

Create a waiver request for a package blocked by a JFrog Curation policy.

**Parameters**:

* `pkg_type`: Package ecosystem type (string, required)
* `pkg_name`: Canonical package name (string, required)
* `pkg_version`: Exact blocked version (string, required)
* `repo_key`: Curation-enabled Artifactory repository key (string, required)
* `reason`: User-provided justification; at least 5 characters (string, required)

### `jfs_curation_query_waiver_requests`

*Available from Xray - 3.148.0.*

Search and check the status of Curation waiver requests.

**Parameters**:

* `status`: Comma-separated statuses — `pending`, `approved`, `rejected` (string, optional)
* `pkg_type`: Package ecosystem type filter; comma-separated for multiple (string, optional)
* `search`: Substring search across package name and version (string, optional)
* `can_approve`: Return only waivers the caller can approve (boolean, optional)
* `approved_status`: Sub-filter for approved waivers — `permanent`, `expiring_soon`, or `expired` (string, optional)
* `decision_owners`: Comma-separated decision-owner group IDs (string, optional)
* `created_at_start`: Creation time lower bound, RFC3339 (string, optional)
* `created_at_end`: Creation time upper bound, RFC3339 (string, optional)
* `updated_at_start`: Last-updated lower bound, RFC3339 (string, optional)
* `updated_at_end`: Last-updated upper bound, RFC3339 (string, optional)
* `order_by`: Sort field — `id`, `created_at`, `updated_at`, `status`, `pkg_type`, `pkg_name`, `pkg_version`, `policies`, or `waiver_expiry` (string, optional)
* `direction`: Sort direction — `asc` or `desc` (string, optional)
* `num_of_rows`: Results per page (integer, optional)
* `page_num`: Page number, 1-based (integer, optional)

</details>

<a id="distribution" name="distribution"></a>
<details>
<summary><b>Distribution</b></summary>

### `distribution_release_bundles_distribute`

*Available from Distribution - 2.37.*

Start a Release Bundle v2 (RBv2) distribution to one or more edge nodes.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `distribution_rules`: Edge-targeting rules. Pass `[{"site_name":"*","city_name":"*","country_codes":["*"]}]` for all edges (object\[], required)
* `project`: Project key; required for project-scoped bundles (string, optional)
* `repository_key`: Override of the storing repository (string, optional)
* `dry_run`: Simulate without distributing (boolean, optional)
* `auto_create_missing_repositories`: Create missing repos on edges (boolean, optional)
* `bypass_xray_scan_result`: Skip Xray block on distribution (boolean, optional)
* `include_evidence`: Replicate evidence alongside artifacts (boolean, optional)
* `modifications`: Edge-side modifications — `read_only`, `default_path_mapping_by_last_promotion`, `mappings` (object, optional)

### `distribution_release_bundles_abort`

*Available from Distribution - 2.19.*

Abort an in-progress distribution. Does not roll back already-transferred files.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `project`: Project key; required for project-scoped bundles (string, optional)
* `repository_key`: Override of the storing repository (string, optional)

### `distribution_release_bundles_get_path_mapping`

*Available from Distribution - 2.20.*

Get the applied path mapping and ATW flag for a release bundle version.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `project`: Project key; required for project-scoped bundles (string, optional)
* `repository_key`: Override of the storing repository (string, optional)
* `distribution_tracker`: Scope to a specific tracker ID (string, optional)

### `distribution_trackers_list`

*Available from Distribution - 2.19.*

List distribution trackers (history) for a release bundle version.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `project`: Project key; required for project-scoped bundles (string, optional)
* `repository_key`: Override of the storing repository (string, optional)

### `distribution_trackers_get_by_id`

*Available from Distribution - 2.19.*

Get per-edge progress for a specific distribution tracker.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `tracker_id`: Long numeric tracker ID from the distribute response (string, required)

### `distribution_signing_keys_get_for_bundle`

*Available from Distribution - 2.23.*

Get signing keys associated with a release bundle version.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `project`: Project key; required for project-scoped bundles (string, optional)
* `repository_key`: Override of the storing repository (string, optional)

### `distribution_signing_keys_get_public`

*Available from Distribution - 2.19.*

Retrieve the public part of a Distribution signing key as PEM.

**Parameters**:

* `key_name`: Signing key alias (string, required)

### `distribution_signing_keys_propagate`

*Available from Distribution - 2.19.*

Push a public signing key to every edge node.

**Parameters**:

* `key_name`: Signing key alias (string, required)

### `distribution_edges_list_for_bundle`

*Available from Distribution - 2.26.*

List edge nodes eligible for a release bundle distribution or deletion.

**Parameters**:

* `release_bundle_name`: Release bundle name (string, required)
* `release_bundle_version`: Release bundle version (string, required)
* `action`: Permission code — `x` (distribute), `d` (delete), `r` (read), `w` (write), `n` (annotate), `m` (manage), `a` (admin) (string, required)
* `project`: Project key; required for project-scoped bundles (string, optional)
* `repository_key`: Override of the storing repository (string, optional)

</details>

<a id="workers" name="workers"></a>
<details>
<summary><b>Workers</b></summary>

### `worker_list_all`

*Available from Workers - 1.0.*

List JFrog Workers on the platform.

**Parameters**:

* `project_key`: Project key to list workers for (string, optional)
* `keys_only`: Return only worker keys (boolean, optional)

### `worker_get_specific`

*Available from Workers - 1.0.*

Retrieve the full details of a single JFrog Worker by key.

**Parameters**:

* `worker_key`: Worker key to retrieve (string, required)

### `worker_list_actions`

*Available from Workers - 1.0.*

List JFrog Worker trigger actions.

**Parameters**:

* `project_key`: Project key to scope actions (string, optional)

### `worker_get_instructions_for_code_generation`

Return a code template, type definitions, PlatformContext typings, and best-practice instructions for implementing JFrog Worker code.

**Parameters**:

* `action`: Worker action name from `worker_list_actions` (string, required)
* `intended_purpose`: Short description of what the worker should do (string, required)

### `worker_create`

*Available from Workers - 1.0.*

Create a new JFrog Worker. The worker is created disabled.

**Parameters**:

* `name`: Worker key (string, required)
* `action_name`: Trigger action name from `worker_list_actions` (string, required)
* `action_application`: Application paired with the action (string, required)
* `worker_code`: Full TS/JS worker source; prefix with `base64:` if encoded (string, required)
* `project_key`: Access project key (string, optional)
* `description`: Human-readable description (string, optional)
* `filter_criteria`: Action-specific filter criteria object (object, optional)
* `secrets`: Worker secrets as key/value objects (object\[], optional)
* `properties`: Worker properties as key/value objects (object\[], optional)
* `shared`: Allow non-admin execution where permitted (boolean, optional)
* `debug`: Record successful executions for visibility (boolean, optional)

### `worker_update`

*Available from Workers - 1.0.*

Update an existing JFrog Worker. Prefer loading the current state with `worker_get_specific` first.

**Parameters**:

* `name`: Worker key (string, required)
* `action_name`: Trigger action name from `worker_list_actions` (string, required)
* `action_application`: Application paired with the action (string, required)
* `worker_code`: Full TS/JS worker source; prefix with `base64:` if encoded (string, required)
* `enabled`: Whether the worker is enabled (boolean, optional)
* `project_key`: Access project key (string, optional)
* `description`: Human-readable description (string, optional)
* `filter_criteria`: Action-specific filter criteria object (object, optional)
* `secrets`: Worker secrets as key/value objects (object\[], optional)
* `properties`: Worker properties as key/value objects (object\[], optional)
* `shared`: Allow non-admin execution where permitted (boolean, optional)
* `debug`: Record successful executions for visibility (boolean, optional)

### `worker_get_execution_history`

*Available from Workers - 1.0.*

Retrieve execution history for JFrog Workers.

**Parameters**:

* `worker_key`: Filter to a specific worker key (string, optional)
* `project_key`: Filter to workers in a project (string, optional)
* `show_test_run`: Include test runs (boolean, optional)
* `max_items`: Maximum history entries to return (integer, optional)
* `start`: Exclude executions before this epoch ms timestamp (integer, optional)
* `end`: Exclude executions after this epoch ms timestamp (integer, optional)

</details>

<a id="event" name="event"></a>
<details>
<summary><b>Event</b></summary>

### `event_domains_list`

List the webhook domain and event type catalog on the JFrog Event service.

**Parameters**:

* `project_key`: Project key for auth context only; does not filter the catalog (string, optional)

### `event_subscriptions_list`

List webhook subscriptions the caller can read.

**Parameters**:

* `project_key`: Project key to scope results (string, optional)
* `domain`: Filter by event domain ids from `event_domains_list` (string\[], optional)

### `event_subscriptions_get`

Get one webhook subscription by key.

**Parameters**:

* `subscription_key`: Subscription key to retrieve (string, required)
* `project_key`: Project key for project-scoped subscriptions (string, optional)

### `event_subscriptions_create`

Create a new webhook subscription. Prefer verifying domain and event types with `event_domains_list` first.

**Parameters**:

* `subscription_key`: Subscription key for the new webhook (string, required)
* `domain`: Event domain id from `event_domains_list` (string, required)
* `event_types`: Event type ids from `event_domains_list` (string\[], required)
* `handlers`: Handler config array with exactly one entry (object\[], required)
* `enabled`: Whether the subscription is active on create; default false (boolean, optional)
* `filter_criteria`: Event filter criteria object (object, optional)
* `description`: Human-readable description (string, optional)
* `project_key`: Project scope when all chosen event types support projects (string, optional)
* `debug`: Record webhook execution details (boolean, optional)
* `force`: Skip handler URL verification only (boolean, optional)

### `event_subscriptions_update`

Update an existing webhook subscription (full replace). Prefer loading the current config with `event_subscriptions_get` first.

**Parameters**:

* `subscription_key`: Subscription key to update (string, required)
* `enabled`: Whether the subscription is active (boolean, required)
* `domain`: Event domain id (string, required)
* `event_types`: Event type ids (string\[], required)
* `handlers`: Full handler array (object\[], required)
* `filter_criteria`: Event filter criteria object (object, optional)
* `description`: Human-readable description (string, optional)
* `project_key`: Project scope; immutable on update (string, optional)
* `debug`: Record webhook execution details (boolean, optional)
* `force`: Skip handler URL verification only (boolean, optional)

</details>

<a id="evidence-config" name="evidence-config"></a>
<details>
<summary><b>Evidence: Config</b></summary>

### `evidence_config_get`

*Available from Evidence - 7.277.*

Retrieve the Evidence service configuration exposed to clients.

**Parameters**:

* No parameters required

### `evidence_config_get_categories`

*Available from Evidence - 7.277.*

Retrieve the full Evidence category configuration.

**Parameters**:

* No parameters required

### `evidence_config_update_categories`

*Available from Evidence - 7.277.*

Replace the Evidence categories configuration.

**Parameters**:

* `categories`: Complete category-to-predicate-type mapping (object, required)

</details>

<a id="evidence-categories" name="evidence-categories"></a>
<details>
<summary><b>Evidence: Categories</b></summary>

### `evidence_categories_list`

*Available from Evidence - 7.277.*

List the predicate categories supported by JFrog Evidence.

**Parameters**:

* No parameters required

### `evidence_categories_get_predicate_types`

*Available from Evidence - 7.277.*

Retrieve all predicate type URIs that belong to a specific Evidence category.

**Parameters**:

* `category`: Category name to retrieve predicate types for (string, required)

</details>

<a id="evidence-records" name="evidence-records"></a>
<details>
<summary><b>Evidence: Records</b></summary>

### `evidence_records_search`

*Available from Evidence - 7.277.*

Search for evidence records by repository, subject path, subject name, or SHA-256.

**Parameters**:

* `repository_key`: Artifactory repository key to scope the search (string, required)
* `path`: Subject path within the repository (string, optional)
* `name`: Subject artifact file name (string, optional)
* `sha256`: Subject SHA-256 digest (string, optional)
* `limit`: Maximum number of results to return (integer, optional)
* `offset`: Number of results to skip for pagination (integer, optional)

### `evidence_records_get_by_subject`

*Available from Evidence - 7.277.*

List all evidence records attached to a specific subject.

**Parameters**:

* `selector`: Repository-qualified subject path (string, required)
* `sha256`: Subject SHA-256 digest to disambiguate versions (string, optional)
* `predicate_categories`: Comma-separated predicate categories to filter by (string, optional)
* `include`: Extra fields to inline, e.g. `predicates`, `signatures`, or `predicates,signatures` (string, optional)

### `evidence_records_get_by_id`

*Available from Evidence - 7.277.*

Retrieve a single evidence record by its unique ID.

**Parameters**:

* `id`: Unique evidence ID (string, required)
* `include`: Extra fields to inline, e.g. `predicates`, `signatures`, or `predicates,signatures` (string, optional)

### `evidence_records_get_markdown_by_id`

*Available from Evidence - 7.289.*

Retrieve the human-readable Markdown rendering of a single evidence record.

**Parameters**:

* `id`: Unique evidence ID (string, required)

### `evidence_records_prepare_statement`

*Available from Evidence - 7.277.*

Prepare a ready-to-sign in-toto statement for a JFrog subject.

**Parameters**:

* `predicate`: Predicate body as a plain JSON object (object, required)
* `predicate_type`: Predicate type URI (string, required)
* `subject_type`: Subject kind, e.g. `artifact`, `build`, `package`, `release_bundle`, or `application_version` (string, required)
* `markdown`: Human-readable Markdown summary of the evidence (string, optional)
* `provider_id`: Provider identifier to associate with the evidence (string, optional)
* `project_key`: JFrog Project key to associate the evidence with (string, optional)
* `subject_sha256`: Subject SHA-256 digest (string, optional)
* `repo_path`: Repo-qualified artifact path; required when subject\_type is `artifact` (string, optional)
* `build_name`: Build name; required when subject\_type is `build` (string, optional)
* `build_number`: Build number; required when subject\_type is `build` (string, optional)
* `build_timestamp`: Build timestamp to disambiguate builds (string, optional)
* `release_bundle_name`: Release bundle name; required when subject\_type is `release_bundle` (string, optional)
* `release_bundle_version`: Release bundle version; required when subject\_type is `release_bundle` (string, optional)
* `application_key`: Application key; required when subject\_type is `application_version` (string, optional)
* `application_version`: Application version; required when subject\_type is `application_version` (string, optional)
* `package_repo`: Package repository; required when subject\_type is `package` (string, optional)
* `package_name`: Package name; required when subject\_type is `package` (string, optional)
* `package_version`: Package version; required when subject\_type is `package` (string, optional)
* `attachments`: Attachment files stored in Artifactory (object\[], optional)
* `include_pae`: Set to `true` to include DSSE Pre-Authentication Encoding bytes (string, optional)

### `evidence_records_create_by_subject`

*Available from Evidence - 7.277.*

Upload an already-signed DSSE envelope as evidence and attach it to a JFrog subject.

**Parameters**:

* `selector`: Repository-qualified subject path (string, required)
* `payload`: DSSE envelope payload field (string, required)
* `payload_type`: DSSE envelope payload type (string, required)
* `signatures`: DSSE envelope signatures (object\[], required)
* `attachments`: Additional artifacts to attach alongside this evidence (object\[], optional)
* `provider_id`: Provider identifier to associate with the evidence (string, optional)

</details>

<a id="jfrog-apptrust" name="jfrog-apptrust"></a>
<details>
<summary><b>JFrog AppTrust</b></summary>

### `apptrust_create_application`

Create a new JFrog AppTrust application.

**Parameters**:

* `application_key`: Unique application identifier (string, required)
* `application_name`: Display name (string, required)
* `project_key`: Project key (string, required)
* `description`: Application description (string, optional)
* `maturity_level`: Maturity level — unspecified, experimental, production, end\_of\_life (string, optional)
* `criticality`: Criticality — unspecified, low, medium, high, critical (string, optional)
* `labels`: Key-value metadata labels (object\[], optional)
* `user_owners`: User owner names (string\[], optional)
* `group_owners`: Group owner names (string\[], optional)

### `apptrust_get_application_summary`

Get details of a JFrog AppTrust application.

**Parameters**:

* `application_key`: Application identifier (string, required)

### `apptrust_list_applications`

List JFrog AppTrust applications with filtering.

**Parameters**:

* `project_key`: Filter by project (string, optional)
* `name`: Substring filter on display name (string, optional)
* `criticality`: Criticality filter (string, optional)
* `maturity_level`: Maturity level filter (string, optional)
* `label`: Label filters as `key:value` (string\[], optional)
* `owner`: Owner name filters (string\[], optional)
* `limit`: Page size (integer, optional)
* `offset`: Pagination offset (integer, optional)
* `order_by`: Sort field — `name` or `created` (string, optional)
* `order_asc`: Ascending sort order (boolean, optional)

### `apptrust_create_application_version`

Create a new version of a JFrog AppTrust application.

**Parameters**:

* `application_key`: Parent application identifier (string, required)
* `version`: Semantic version string (string, required)
* `sources`: Content sources — builds, packages, artifacts, release bundles, AQL, or other app versions (object, required)
* `tag`: Version tag (string, optional)
* `filters`: Include/exclude filters (object, optional)
* `draft`: Create as draft version (boolean, optional)
* `async_`: Run creation asynchronously (boolean, optional)
* `sign_key_name`: Signing key name (string, optional)

### `apptrust_list_versions`

List versions of a JFrog AppTrust application.

**Parameters**:

* `application_key`: Application identifier (string, required)
* `release_status`: Filter — `PRE_RELEASE`, `RELEASED`, or `TRUSTED_RELEASE` (string, optional)
* `tag`: Tag filter (string, optional)
* `order_by`: Sort field (string, optional)
* `order_asc`: Ascending sort order (boolean, optional)
* `limit`: Page size (integer, optional)
* `offset`: Pagination offset (integer, optional)

### `apptrust_get_application_version_status`

Get the release status for a specific application version.

**Parameters**:

* `application_key`: Application identifier (string, required)
* `version`: Version string (string, required)

### `apptrust_get_lifecycle_overview`

Get lifecycle stages configuration for a project.

**Parameters**:

* `project_key`: Project key (string, required)
* `filter_gates_by`: Filter gates — `policies` (string, optional)

### `apptrust_promote_version`

Promote an application version to a lifecycle stage.

**Parameters**:

* `application_key`: Application identifier (string, required)
* `version`: Version string (string, required)
* `target_stage`: Target lifecycle stage (string, required)
* `promotion_type`: Promotion type — move, copy, keep, dry\_run (string, optional)
* `included_repository_keys`: Repositories to include (string\[], optional)
* `excluded_repository_keys`: Repositories to exclude (string\[], optional)
* `overwrite_strategy`: Overwrite strategy — DISABLED, LATEST, ALL (string, optional)
* `async_`: Run promotion asynchronously (boolean, optional)
* `sign_key_name`: Signing key name (string, optional)

### `apptrust_get_version_promotion_history`

Get all promotions for a specific application version.

**Parameters**:

* `application_key`: Application identifier (string, required)
* `version`: Version string (string, required)
* `limit`: Max records (integer, optional)
* `offset`: Pagination offset (integer, optional)

### `apptrust_release_version`

Release an application version to the PROD stage.

**Parameters**:

* `application_key`: Application identifier (string, required)
* `version`: Version string (string, required)
* `promotion_type`: Promotion type — move, copy, keep, dry\_run (string, optional)
* `included_repository_keys`: Repositories to include (string\[], optional)
* `excluded_repository_keys`: Repositories to exclude (string\[], optional)
* `overwrite_strategy`: Overwrite strategy — DISABLED, LATEST, ALL (string, optional)
* `async_`: Run release asynchronously (boolean, optional)
* `sign_key_name`: Signing key name (string, optional)

### `apptrust_rollback_version`

Roll back the latest promotion of an application version.

**Parameters**:

* `application_key`: Application identifier (string, required)
* `version`: Version string (string, required)
* `from_stage`: Stage to roll back from (string, required)
* `async_`: Run rollback asynchronously (boolean, optional)

### `apptrust_get_activity_logs`

Get activity log events from JFrog AppTrust.

**Parameters**:

* `application_key`: Filter by application key (string, optional)
* `project_key`: Filter by project key (string, optional)
* `application_name`: Filter by application names (string\[], optional)
* `project_name`: Filter by project names (string\[], optional)
* `timestamp_from`: Start time in unix milliseconds (integer, optional)
* `timestamp_to`: End time in unix milliseconds (integer, optional)
* `subject_id`: Filter by subject ID (string, optional)
* `subject_name`: Filter by subject name (string, optional)
* `created_by`: Filter by creator usernames (string\[], optional)
* `limit`: Page size (integer, optional)
* `offset`: Pagination offset (integer, optional)
* `sort_by`: Sort field (string, optional)
* `order`: Sort order — `asc` or `desc` (string, optional)

</details>
