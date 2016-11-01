hugo-aws-infra
=========

This Ansible role will create all necessary Amazon AWS resources you need to host your site generated using [Hugo](https://gohugo.io) ... serverless.

Requirements
------------
You'll need the following stuff to get started:

* ansible >= 2.1.x
* aws-cli >= 1.11.x
* [Amazon AWS account](https://aws.amazon.com/free)

**Note:** before you run `ansible-playbook`, make sure `boto` has access to your AWS profile (~ for example by exporting the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables).

TL;DR
------------

See [this](https://www.foobar-it.com/2016/09/03/hello-hugo/) blog post.

Use a playbook like this:

```sh
---
  - name: Create Hugo infra on Amazon AWS
    hosts: localhost
    gather_facts: true

    vars:
      website_domain: foobar-it.com
      verbose_output: true

    roles:
      - role: hugo-aws-infra
        s3_website_domain: "{{ website_domain }}"
        verbose: "{{ verbose_output }}"
        tags:
          - infra
```

Run:

```sh
$ ansible-playbook -i localhost site.yml
```

Where: `site.yml` contains the contents I pasted above.

As a result, the following resources are created:

* An ACM certificate is requested and (after manually approval) issued ;
* A properly configured S3 bucket for all Hugo artifacts ... including Bucket Policy ;
* A CloudFront Distribution which caches all S3 objects ;
* A public hosted zone in Route53 ;
* And finally, a set of DNS records that point to the CloudFront Distribution


License
-------

BSD
