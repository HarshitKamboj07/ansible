ansible_azure_config/
├── ansible.cfg
├── collections/
│ └── requirements.yml
├── inventories/
│ ├── dev/
│ │ ├── group_vars/
│ │ │ ├── all.yml
│ │ │ ├── linux.yml
│ │ │ └── windows.yml
│ │ └── azure_rm.yml
│ └── prod/
│ ├── group_vars/
│ │ ├── all.yml
│ │ ├── linux.yml
│ │ └── windows.yml
│ └── azure_rm.yml
├── roles/
│ └── notepad_plus_plus/
└── README.md# Azure Infrastructure Management with Ansible

Enterprise-grade Ansible configuration for managing Azure infrastructure.

## Directory Structure

```
ansible_azure_config/
├── ansible.cfg                 # Global Ansible configuration
├── collections/               # Ansible collections
│   └── requirements.yml      # Collection dependencies
├── credentials/              # Encrypted credentials (vault)
│   └── azure_creds.yml      # Azure credentials
├── inventories/             # Environment inventories
│   ├── prod/               # Production environment
│   │   ├── group_vars/    # Production variables
│   │   ├── host_vars/     # Host-specific variables
│   │   ├── azure_rm.yml   # Azure dynamic inventory
│   │   └── hosts.yml      # Static inventory
│   └── dev/               # Development (similar structure)
├── inventory_plugins/       # Custom inventory plugins
├── molecule/               # Testing framework
├── playbooks/             # Task playbooks
└── roles/                 # Ansible roles
```

## Prerequisites

1. Install required packages:

```bash
python -m pip install --upgrade pip
pip install ansible-core azure-cli ansible[azure] molecule molecule-azure yamllint ansible-lint
```

2. Install Ansible collections:

```bash
ansible-galaxy collection install -r collections/requirements.yml
```

3. Configure Azure credentials:

```bash
az login
az account set --subscription "Your-Subscription-Name"
```

4. Set up pre-commit hooks:

```bash
pip install pre-commit
pre-commit install
```

## Usage

1. Environment Setup:

```bash
cp .env.example .env
# Edit .env with your values
```

2. Encrypt sensitive files:

```bash
ansible-vault encrypt credentials/azure_creds.yml
```

3. Test dynamic inventory:

```bash
ansible-inventory --list
```

4. Run playbooks:

```bash
# Production
ansible-playbook playbooks/windows_software.yml -i inventories/prod

# Development
ansible-playbook playbooks/windows_software.yml -i inventories/dev
```

5. Run tests:

```bash
molecule test
```

## Best Practices Implemented

1. **Security**

   - Vault encryption for sensitive data
   - Pre-commit hooks for security checks
   - Environment-based credentials
   - Secure connection defaults

2. **Performance**

   - Fact caching enabled
   - SSH pipelining
   - Optimized fork count
   - Smart gathering

3. **Maintainability**

   - Clear directory structure
   - Environment separation
   - Role-based organization
   - Consistent naming

4. **Testing**

   - Molecule integration
   - Linting configuration
   - YAML validation
   - Automated testing

5. **Azure Integration**

   - Dynamic inventory
   - Tag-based filtering
   - Resource-based grouping
   - Environment separation

6. **Version Control**
   - .gitignore configuration
   - Pre-commit hooks
   - Documentation
   - Requirements tracking

## Contributing

1. Fork the repository
2. Create a feature branch
3. Run pre-commit hooks
4. Run molecule tests
5. Submit pull request

## Security Notes

- Never commit unencrypted credentials
- Rotate credentials regularly
- Use least privilege access
- Enable audit logging
- Regular security updates

## Testing

- Run molecule tests before commits
- Test in development first
- Validate idempotency
- Check syntax and linting

## Maintenance

- Regular collection updates
- Security patches
- Documentation updates
- Credential rotation
