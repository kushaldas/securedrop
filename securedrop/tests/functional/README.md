### To test in prod vms

- `sudo -u www-data bash`
- `cd /var/wwww/securedrop/`
- `./manage.py reset`    # This will clean the DB for testing
- `./create-demo-user.py`  

Update this information to the `tests/functional/instance_infomration.json file.

The content of the file looks like below.

```
{
    "hidserv_token": "asfjsdfag",
    "journalist_location": "http://thejournalistfqb.onion",
    "source_location": "http://thesourceadsfa.onion",
    "sleep_time": 10,
    "user": {
        "name": "journalist",
        "password": "WEjwn8ZyczDhQSK24YKM8C9a",
        "secret": "JHCOGO7VCER3EJ4L"
    }
}
```

### Run the tests

Go inside of the securedrop directory.

```
$ ./bin/dev-shell ./bin/run-test --capture=no -v tests/functional/test_source_not_found.py
```

Remember to use to pipe to less, or less in case of a failure, there will be too much output.

- `functional/test_source_warnings.py`: THis will fail as we are actually using Tor Browser :)
- `functional/test_submission_not_in_memory.py`: Not inside of the server, so does not make sense.
- `functional/test_source_session_timeout.py`: Remember to change the session time in the server to 0.02 before testing this.
