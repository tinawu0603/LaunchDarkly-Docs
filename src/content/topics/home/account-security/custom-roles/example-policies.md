---
title: "Example policies"
excerpt: ""
---
## Overview
This topic shows some examples of different types of policies you can implement with custom roles. It also provides a reference for different actions you can configure in a policy.
<Callout intent="info">
  <Callout.Title>Creating private projects with custom roles</Callout.Title>
   <Callout.Description>Use the `viewProject` action to allow or deny viewing and editing access to projects. 
To learn more, read [Configuring private projects with custom roles](./configuring-private-projects-with-custom-roles).</Callout.Description>
</Callout>

## Granting access to specific environments and flags
This example policy allows members of the QA team to administer environments tagged `qa_*` and manage flags in environments tagged `qa_*`.
[block:code]
{
  "codes": [
    {
      "code": "[\n  {\n    \"effect\": \"allow\",\n    \"resources\": [\"proj/*:env/*;qa_*\"],\n    \"actions\": [\"*\"]\n  },\n  {\n    \"effect\": \"allow\",\n    \"resources\": [\"proj/*:env/*;qa_*:/flag/*\"],\n    \"actions\": [\"*\"]\n  }\n]",
      "language": "json",
      "name": "QA team policy"
    }
  ]
}
[/block]

## Granting access to kill switch features, but not flag rollout or targeting rules
This example policy allows members of the ops team to kill switch features on the production environment. They may not change percentage rollouts or targeting rules, or manage any environments or projects.
[block:code]
{
  "codes": [
    {
      "code": "[\n  {\n    \"effect\": \"allow\",\n    \"resources\": [\"proj/*:env/production:flag/*\"],\n    \"actions\": [\"updateOn\"]\n  }\n]\n",
      "language": "json",
      "name": "Ops team"
    }
  ]
}
[/block]