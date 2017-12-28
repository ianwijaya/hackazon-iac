
please change vars.yml before starting the playbook.
if you want to install the db within the same host, use 'localhost' instead as mysql_host

# Project Title

Deploying Hackazon and WAF protection in Multi-Cloud Environment

## What is this

Hackazon is modern vulnerable web application. Just like many web and mobile applications as well as web services, most of them are not being adequately tested for security vulnerabilities. Wherever the apps may move, these vulnerabilities will also follow.
WAAP is one of the popular and fastest solution to patch and protect these vulnerabilities.

This repository shows:
  1. How we can automate Hackazon deployment in multi-cloud Environment
  2. How we can also automate WAAP deployment and transition the protection quickly to operations (SecOps)
  3. How we can scale within the cloud AND across the clouds with ADC technology


This repo contains Ansible script to deploy just that in Multi Cloud environment.

### Prerequisites

You need 1 machine as ansible master (this can be your computer or another server)

```
Give examples
```

### Installing

A step by step series of examples that tell you have to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags).

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
