# Bosh release for Docker

One of the fastest ways to get [Docker](https://www.docker.io/) and orchestrate containers with persistent data on any infrastructure is to deploy this BOSH release.

## Disclaimer

This is not presently a production ready [Docker](https://www.docker.io/) BOSH release. This is a work in progress.

This BOSH release needs a [BOSH stemcell](http://bosh_artifacts.cfapps.io/file_collections?type=stemcells) with a embedded Linux kernel >= 3.8. At this moment the official stemcells come with Linux kernel 3.0, so for your convenience here there are the links to some unofficial stemcells:

* AWS: [http://storage.googleapis.com/bosh-stemcells/bosh-stemcell-2005-aws-xen-ubuntu-3.8.tgz](http://storage.googleapis.com/bosh-stemcells/bosh-stemcell-2005-aws-xen-ubuntu-3.8.tgz)
* OpenStack: [http://storage.googleapis.com/bosh-stemcells/bosh-stemcell-2005-openstack-kvm-ubuntu-3.8.tgz](http://storage.googleapis.com/bosh-stemcells/bosh-stemcell-2005-openstack-kvm-ubuntu-3.8.tgz)
* VSphere: [http://storage.googleapis.com/bosh-stemcells/bosh-stemcell-2005-vsphere-esxi-ubuntu-3.8.tgz](http://storage.googleapis.com/bosh-stemcells/bosh-stemcell-2005-vsphere-esxi-ubuntu-3.8.tgz)
* GCE: [http://storage.googleapis.com/bosh-stemcells/light-bosh-stemcell-2005-google-kvm-ubuntu.tgz](http://storage.googleapis.com/bosh-stemcells/light-bosh-stemcell-2005-google-kvm-ubuntu.tgz)

## Usage

### Upload the BOSH release

To use this BOSH release, first upload it to your BOSH:

```
bosh target BOSH_HOST
git clone https://github.com/cf-platform-eng/docker-boshrelease.git
cd docker-boshrelease
bosh upload release releases/docker-2.yml
```

### Create a BOSH deployment manifest

Now create a deployment file (using the files at the [examples](https://github.com/cf-platform-eng/docker-boshrelease/tree/master/examples) directory as a starting point) and deploy:

```
vi path/to/deployment.yml
bosh deployment path/to/deployment.yml
bosh -n deploy
```

## Create new final release

To create a new final release you need to get read/write API credentials to the [@cloudfoundry-community](https://github.com/cloudfoundry-community) s3 account.

Please email [Dr Nic Williams](mailto:&#x64;&#x72;&#x6E;&#x69;&#x63;&#x77;&#x69;&#x6C;&#x6C;&#x69;&#x61;&#x6D;&#x73;&#x40;&#x67;&#x6D;&#x61;&#x69;&#x6C;&#x2E;&#x63;&#x6F;&#x6D;) and he will create unique API credentials for you.

Create a `config/private.yml` file with the following contents:

``` yaml
---
blobstore:
  s3:
    access_key_id:     ACCESS
    secret_access_key: PRIVATE
```

You can now create final releases for everyone to enjoy!

```
bosh create release
# test this dev release
git commit -m "updated docker"
bosh create release --final
git commit -m "creating vXYZ release"
git tag vXYZ
git push origin master --tags
```

## Contributing

In the spirit of [free software](http://www.fsf.org/licensing/essays/free-sw.html), **everyone** is encouraged to help improve this project.

Here are some ways *you* can contribute:

* by using alpha, beta, and prerelease versions
* by reporting bugs
* by suggesting new features
* by writing or editing documentation
* by writing specifications
* by writing code (**no patch is too small**: fix typos, add comments, clean up inconsistent whitespace)
* by refactoring code
* by closing [issues](https://github.com/cf-platform-eng/docker-boshrelease/issues)
* by reviewing patches


### Submitting an Issue
We use the [GitHub issue tracker](https://github.com/cf-platform-eng/docker-boshrelease/issues) to track bugs and features.
Before submitting a bug report or feature request, check to make sure it hasn't already been submitted. You can indicate
support for an existing issue by voting it up. When submitting a bug report, please include a
[Gist](http://gist.github.com/) that includes a stack trace and any details that may be necessary to reproduce the bug,
including your gem version, Ruby version, and operating system. Ideally, a bug report should include a pull request with
 failing specs.


### Submitting a Pull Request

1. Fork the project.
2. Create a topic branch.
3. Implement your feature or bug fix.
4. Commit and push your changes.
5. Submit a pull request.

## Copyright

See [LICENSE](https://github.com/cf-platform-eng/docker-boshrelease/blob/master/LICENSE) for details.
Copyright (c) 2014 [Pivotal Software, Inc](http://www.gopivotal.com/).