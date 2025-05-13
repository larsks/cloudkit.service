# cloudkit.service

This is a demonstration of how you can install Ansible collections via Python packages.

## Usage

1. Create a new project directory:

    ```
    mkdir myproject
    cd myproject
    ```

2. Initialize a `uv` environment:

    ```
    uv init
    ```

3. Install this repository:

    ```
    uv add git+https://github.com/larsks/cloudkit.service
    ```

4. Test out Ansible filters installed by this repository:

    ```
    $ uv run ansible localhost -m debug -a 'msg="{{ \"one/two/three\" | cloudkit.service.json_pointer_escape }}"'
    localhost | SUCCESS => {
        "msg": "one~1two~1three"
    }
    ```

5. Test out playbooks and roles installed by this repository:

    ```
    $ cat > playbook.yaml <<EOF
    - hosts: localhost
      gather_facts: false
      roles:
      - cloudkit.service.testrole

    - name: Run playbook from a collection
      ansible.builtin.import_playbook: cloudkit.service.testplaybook
    EOF
    $ uv run ansible-playbook playbook.yaml
    ```
