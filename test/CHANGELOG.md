## [_Unreleased_](https://github.com/freckle/platform/compare/v2.2.1.0...main)

## [v2.2.1.0](https://github.com/freckle/platform/compare/v2.2.0.0...v2.2.1.0)

- Support a single `.platform.yaml`

  The following,

  ```yaml
  # $app/.platform/$resource-a.yaml
  inputs: a
  environments: b
  uses: x
  with: y

  # $app/.platform/$resource-b.yaml
  inputs: a
  environments: b
  uses: x
  with: y
  ```

  can now be simplified to,

  ```yaml
  # $app/.platform.yaml
  inputs: a
  environments: b
  resources:
    - name: $resource-a
      uses: x
      with: y
    - name: $resource-b
      uses: x
      with: y
  ```

  **NOTE**: you are encouraged to move to this style, support for separate
  resource files will be deprecated and removed in a future version.

- Support multiple arguments to `query`

  ```
  platform query x y

  # Behaves the same as
  platform query x
  platform query y
  ```

## [v2.2.0.0](https://github.com/freckle/platform/compare/v2.1.0.20...v2.2.0.0)

- Removed `query.StackTemplate` and `query.StackParameters`

  These are no longer used now that we're Stackctl-based.

NOTE: This is a breaking change and thus a major version bump, but we're
unlikely to be relying on this anywhere, so upgrades should be very safe.

## [v2.1.0.20](https://github.com/freckle/platform/compare/v2.1.0.19...v2.1.0.20)

No-op release to trigger re-building of executables.

## [v2.1.0.19](https://github.com/freckle/platform/compare/v2.1.0.18...v2.1.0.19)

- Fix bug with removed `deploy --inspect` functionality

  This likely regressed with v2.1.0.12. We now generate a StackSpec can
  (effectively) call `stackctl cat` on it.

## [v2.1.0.18](https://github.com/freckle/platform/compare/v2.1.0.17...v2.1.0.18)

- Ensure `Environment` lists don't duplicate names

  If you put a `container.environment.{Name}` value that already exists in the
  underlying template, your value will be respected. Previously, both would be
  included and you would receive a validation error on deployment.

## [v2.1.0.17](https://github.com/freckle/platform/compare/v2.1.0.16...v2.1.0.17)

- Fix scheduled tasks unable to read DatadogApiKey from SSM

## [v2.1.0.16](https://github.com/freckle/platform/compare/v2.1.0.15...v2.1.0.16)

- Update `stackctl` dependency to fix bug causing Throttling errors.

## [v2.1.0.15](https://github.com/freckle/platform/compare/v2.1.0.14...v2.1.0.15)

- Fix release task

## [v2.1.0.14](https://github.com/freckle/platform/compare/v2.1.0.13...v2.1.0.14)

- Fix another packaging bug

## [v2.1.0.13](https://github.com/freckle/platform/compare/v2.1.0.12...v2.1.0.13)

- Fix packaging bugs on clean builds

## [v2.1.0.12](https://github.com/freckle/platform/compare/v2.1.0.11...v2.1.0.12)

- Don't tag Stacks with version; churning this tag on all resources doesn't work
  in a continuous-deployment context

- Extract all specification-handling to a separate Stackctl project

  https://github.com/freckle/stackctl

  Removes all `spec:` commands. If you were relying on these, install and use
  `stackctl` directly.

## [v2.1.0.11](https://github.com/freckle/platform/compare/v2.1.0.10...v2.1.0.11)

- Pull DatadogApiKey from AWS SSM

## [v2.1.0.10](https://github.com/freckle/platform/compare/v2.1.0.9...v2.1.0.10)

- Error if more than one specification produces the same Stack name

## [v2.1.0.9](https://github.com/freckle/platform/compare/v2.1.0.8...v2.1.0.9)

- Fix PR formatting of metadata-only changes
- Add a warning when no specs are discovered

## [v2.1.0.8](https://github.com/freckle/platform/compare/v2.1.0.7...v2.1.0.8)

- Always require confirmation for automatic deletion on `ROLLBACK_COMPLETE`

## [v2.1.0.7](https://github.com/freckle/platform/compare/v2.1.0.6...v2.1.0.7)

- Automatically handle Stacks in `ROLLBACK_COMPLETE` state
- Don't exit failure on validation errors in `spec:changes`

## [v2.1.0.6](https://github.com/freckle/platform/compare/v2.1.0.5...v2.1.0.6)

- Correctly handle creating change-sets for Stacks that were abandoned during
  their very first change-set.

## [v2.1.0.5](https://github.com/freckle/platform/compare/v2.1.0.4...v2.1.0.5)

- Fix bug preventing creating change-sets for Stacks that don't exist yet
- Catch and print validation errors in change-set creation, instead of letting
  the `_ServiceError` exception crash the program

## [v2.1.0.4](https://github.com/freckle/platform/compare/v2.1.0.3...v2.1.0.4)

- Pass `--filter <generated path>` to `spec:deploy` when used as part of
  `deploy`, to ensure we don't unintentionally deploy other specifications if
  present

## [v2.1.0.3](https://github.com/freckle/platform/compare/v2.1.0.2...v2.1.0.3)

- Documentation updates

## [v2.1.0.2](https://github.com/freckle/platform/compare/v2.1.0.1...v2.1.0.2)

- Documentation updates

## [v2.1.0.1](https://github.com/freckle/platform/compare/v2.1.0.0...v2.1.0.1)

- Print Stack Events during deployment
- Fix bug where we exited zero event if `(spec:)deploy` failed

  Introduced in v2.0 with the move to Amazonka.

## [v2.1.0.0](https://github.com/freckle/platform/compare/v2.0.0.0...v2.1.0.0)

- Make `--tag` required in `spec:generate` and `deploy`
- Remove `cfn-flip` as an executable dependency

  See https://gihub.com/freckle/cfn-flip

## [v2.0.0.0](https://github.com/freckle/platform/compare/v1.6.2.1...v2.0.0.0)

- Replace all uses of aws-cli with Amazonka (2.0) SDK
- Remove `static` App type and `assets:sync` subcommand

## [v1.6.2.1](https://github.com/freckle/platform/compare/v1.6.2.0...v1.6.2.1)

- Stop requiring `App(CertificateArn|Domain)` in non `web` Apps

## [v1.6.2.0](https://github.com/freckle/platform/compare/v1.6.1.1...v1.6.2.0)

- Always talk to Prod/us-east-1 ECR, fixes bug in `container:push --create`
- Add `.Depends` to Stack Spec

## [v1.6.1.0](https://github.com/freckle/platform/compare/v1.6.0.0...v1.6.1.0)

- Add `spec:cat`
- Fix missing documentation
- Fix bug where `service.deployment` was ignored
- Add golden generation testing

## [v1.6.0.0](https://github.com/freckle/platform/compare/v1.5.0.0...v1.6.0.0)

- Remove automatic check for latest version (and `--no-version-check` option)

## [v1.5.0.0](https://github.com/freckle/platform/compare/v1.4.0.3...v1.5.0.0)

- Remove automatic `DeployedBy` Tag

## [v1.4.0.3](https://github.com/freckle/platform/compare/v1.4.0.2...v1.4.0.3)

- Fix bug in deploy causing currently-deployed Template to be re-used.

## [v1.4.0.2](https://github.com/freckle/platform/compare/v1.4.0.1...v1.4.0.2)

- Web template references a fixed dd-agent tag

## [v1.4.0.1](https://github.com/freckle/platform/compare/v1.4.0.0...v1.4.0.1)

- Fix double-prefixed repository bug

## [v1.4.0.0](https://github.com/freckle/platform/compare/v1.3.1.0...v1.4.0.0)

- Add `service.deployment`
- Flip `container:push` auto-creation default
- Use fully-qualified production ECR everywhere
- Removes `EcrRepository` from `query`
- Tag any deployed Stacks with `DeployedBy: PlatformCLI v{version}`

## [v1.3.1.0](https://github.com/freckle/platform/compare/v1.3.0.2...v1.3.1.0)

- Change `spec:deploy --noconfirm` to `--no-confirm`
- Add `--color` option
- Add `--verbose` option
- Add `inputs.AppUnhealthyThresholdCount`
- Add `with.container.mounts`
- Add `with.executionRole`
- Fix handling of non-Fargate `web` Services

## [v1.3.0.2](https://github.com/freckle/platform/compare/v1.3.0.1...v1.3.0.2)

- Fix `--noconfirm` to actually work

## [v1.3.0.1](https://github.com/freckle/platform/compare/v1.3.0.0...v1.3.0.1)

- Fix mishandling of Add resources in Changes

## [v1.3.0.0](https://github.com/freckle/platform/compare/v1.2.4.3...v1.3.0.0)

- Re-implement `deploy` on top of `spec:generate`/`spec:deploy`

  This is behavior-neutral in functionality, but makes the following superficial
  changes:

  - We have fancier changes output during confirmation
  - We generate (as you might guess) _Stack Specifications_ in
    `.platform/specs`, not the `-template.yaml` and `-parameters.json` files as
    previously.
  - We do not clean up these specs post-deploy (you should `.gitignore`)
  - We now clean up Change Sets in AWS post-deploy

- Use `networking` Outputs, don't pass explicit `Parameter`s

  When Apps deploy on this version, there will be changes present in the Change
  Set for any resources that use (e.g.) the `VpcId` `Parameter` (and now use
  `ImportValue: networking-VpcId`). This can appear disruptive, **but no actual
  changes will occur**.

## [v1.2.4.3](https://github.com/freckle/platform/compare/v1.2.4.2...v1.2.4.3)

- Fix inverted `filter` predicate breaking `--filter` (ironic)

## [v1.2.4.2](https://github.com/freckle/platform/compare/v1.2.4.1...v1.2.4.2)

- Fix parsing of `ChangeSet` optional array fields

## [v1.2.4.1](https://github.com/freckle/platform/compare/v1.2.4.0...v1.2.4.1)

- Fix `StackSpecYaml` parsing of optional fields

## [v1.2.4.0](https://github.com/freckle/platform/compare/v1.2.3.1...v1.2.4.0)

- Add `spec:` subcommands

  - `spec:generate`: generate _Stack Specifications_ (see `STACK_SPEC.md`)
  - `spec:changes`: output changes between specifications and deployed state
  - `spec:deploy`: make deployed state match specifications

  In the next release, the `deploy` subcommand will be re-implemented to call
  these subcommands under the hood.

- Support deployments in any region

  Except the Docker registry, which remains as our ECR in us-east-1.

## [v1.2.3.1](https://github.com/freckle/platform/compare/v1.2.3.0...v1.2.3.1)

- Write a `-parameters.json` file for deployment (and persist on `--inspect`)
- Fix documentation (`service.desiredCount` removed in prior version)

## [v1.2.3.0](https://github.com/freckle/platform/compare/v1.2.2.0...v1.2.3.0)

- Add `ENVIRONMENT` variables to app environment for scheduled apps.

## [v1.2.2.0](https://github.com/freckle/platform/compare/v1.2.0.2...v1.2.2.0)

- Update remaining python2.7 lambdas to python3.9
- Fix non-unique TargetGroup naming
- Automatically set `APP_PORT` and `PORT` in web process containers

## [v1.2.0.2](https://github.com/freckle/platform/compare/v1.2.0.1...v1.2.0.2)

- Release automation changes

## [v1.2.0.1](https://github.com/freckle/platform/compare/v1.2.0.0...v1.2.0.1)

- Fix `--resource` for namespaced resources

## [v1.1.4.3](https://github.com/freckle/platform/compare/v1.1.4.3...v1.2.0.0)

- Add `version` subcommand
- Check if running the latest version on startup

  Disable this by passing `--no-check-version`

- Add/use `Resource` Stack Parameter for naming

  NOTE: This will change Stack and resource names for any App with distinct
  Resources. For Apps with only a same-named Resource, such as
  `my-app/.platform/my-app.yaml`, this is behavior-neutral.

## [v1.1.4.3](https://github.com/freckle/platform/compare/v1.1.4.2...v1.1.4.3)

- Fix leading-slash bug with S3Key in serverless deploys

## [v1.1.4.2](https://github.com/freckle/platform/compare/v1.1.4.1...v1.1.4.2)

- Add `ENVIRONMENT` and `SERVICE` variables to app environment to deal with
  bugs in Datadog.

## [v1.1.4.1](https://github.com/freckle/platform/compare/v1.1.4.0...v1.1.4.1)

- Release bump

## [v1.1.4.0](https://github.com/freckle/platform/compare/v1.1.3.2...v1.1.4.0)

- Add default Datadog env vars to web template.

## [v1.1.3.2](https://github.com/freckle/platform/compare/v1.1.3.1...v1.1.3.2)

- Remove DesiredCount from web template

## [v1.1.3.1](https://github.com/freckle/platform/compare/v1.1.3.0...v1.1.3.1)

- Update Datadog image digest

## [v1.1.3.0](https://github.com/freckle/platform/compare/v1.1.2.1...v1.1.3.0)

- Add using:scheduled resource type
- Add container.secrets configuration to web template
- Fix Role reference in web template

## [v1.1.2.1](https://github.com/freckle/platform/compare/v1.1.2.0...v1.1.2.1)

- Couple web TargetGroup to LoadBalancer by Name, to ensure replacement

## [v1.1.2.0](https://github.com/freckle/platform/compare/v1.1.1.0...v1.1.2.0)

- Add `settings.` to `query` sub-command
- Check for empty `SNSTopicArn` before trying to grab region

## [v1.1.1.0](https://github.com/freckle/platform/compare/v1.1.0.0...v1.1.1.0)

- Don't explicitly name LoadBalancers in web template
- Add platform section in Resource template
- Add AppHealthCheckPath to web template

## [v1.1.0.0](https://github.com/freckle/platform/compare/v1.0.3.0...v1.1.0.0)

- Add `static` AppResource type
- Add `query` sub-command
- Add `assets` sub-commands
- Clarify the difference between App and AppResource

  ```
  {app}/.platform/{resource}.yaml
  ```

  Not

  ```
  {ignored}/.platform/{app}.yaml
  ```

- Move some common options to top-level

  ```
  platform --environment x deploy
  ```

  Not

  ```
  platform deploy --environment x
  ```

## [v1.0.3.0](https://github.com/freckle/platform/compare/v1.0.2.0...v1.0.3.0)

- Add support for policy attachment
- Only wire in SNSEvents to lambdas when a topic ARN is given
- Remove Serverless Application Model
- Add ability to specify HTTP Path
- Update `DatadogAgentImage`

## [v1.0.2.0](https://github.com/freckle/platform/compare/v1.0.1.1...v1.0.2.0)

- Add `serverless` application type

## [v1.0.1.1](https://github.com/freckle/platform/compare/v1.0.1.0...v1.0.1.1)

- Documentation update

## [v1.0.1.0](https://github.com/freckle/platform/compare/v1.0.0.0...v1.0.1.0)

- Add `service.cpuScaling` configuration and `alarms` configuration to `web` App
  type. Deploy AutoScaling, Alarms, and a Dashboard.
- Remove `rain`, because it doesn't support `aws sso`-style logins. Replaced
  with raw `aws-cloudformation` commands. Some deploy UX features were lost in
  this conversion, but will be brought back in a future release

## [v1.0.0.0](https://github.com/freckle/platform/compare/v0.0.0.2...v1.0.0.0)

None. Cut v1 release from 0.0.0.2-rc1.

## [v0.0.0.2](https://github.com/freckle/platform/compare/v0.0.0.1...v0.0.0.2)

- No longer ignore input parameters when existing values were set

## [v0.0.0.1](https://github.com/freckle/platform/tree/v0.0.0.1)

First release
