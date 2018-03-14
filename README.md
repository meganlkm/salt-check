# salt-check

This project is dedicated to testing the logic of salt states, and highstates

* [Install](#install)
* [Docker Examples](#docker-examples)
* [Documentation](docs/README.md)
* [Quick Start](docs/HowTo.md)
* [Development](docs/development.md)

---

## <a name='install'></a> Install

```bash
pip install --editable .
```


## <a name='docker-examples'></a> Docker Examples

This shows how to run docker to test new functions with saltcheck.

#### Run the container:

```bash
[sudo] docker run --rm \
    --add-host=salt:127.0.0.1 \
    -v  $(pwd):/opt/ \
    -v  $(pwd)/salt:/srv/salt \
    -v $(pwd)/pillar:/srv/pillar \
    -v $(pwd)/minion_config/minion:/etc/salt/minion \
    -it wcannon/saltcheck:1.0 bash
```

#### Sync modules:

```bash
# THIS IS TEMPORARY!
mkdir -p /srv/salt/_modules
cp -r /opt/saltcheck /srv/salt/_modules/

salt-call saltutil.sync_modules
salt-call saltcheck -d
```

#### Run some tests:

```bash
salt-call saltcheck.run_state_tests apache
salt-call saltcheck.run_highstate_tests
```
