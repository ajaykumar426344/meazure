# Assuming Roles

For commands that support assuming a role, pass the `-A` flag with a role ARN. You can do this as many times as you'd like and the roles will be assumed in the order passed in.

{% hint style="info" %}
**Note:** You must provide the whole ARN for the role\(s\) to be assumed
{% endhint %}

```bash
# Assume otherRole using credentials from exampleRole
weep metadata exampleRole -A arn:aws:iam::123456789012:role/otherRole

# Assume otherRole then assume andAnother
weep metadata exampleRole -A arn:aws:iam::123456789012:role/otherRole -A arn:aws:iam::123456789012:role/andAnother

# Roles to assume can also be passed as a comma-separated list. This will do the same thing as the previous example
weep metadata exampleRole -A arn:aws:iam::123456789012:role/otherRole,arn:aws:iam::123456789012:role/andAnother
```

When using the ECS credential provider, pass the role\(s\) to be assumed as a comma-separated query-string with the key `assume`:

```bash
AWS_CONTAINER_CREDENTIALS_FULL_URI=http://52.224.111.161:9091/ecs/consoleme_oss_1?assume=arn:aws:iam::123456789012:role/otherRole,arn:aws:iam::123456789012:role/andAnother aws sts get-caller-identity
{
    "UserId": "arn:aws:iam::999049238718:role/consoleme",
    "Account": "AKIA6RG7ZTC7P3BTIHPO",
    "Arn": "arn:aws:iam::999049238718:role/consoleme"
}
```

