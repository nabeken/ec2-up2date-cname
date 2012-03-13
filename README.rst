=================
ec2-up2date-cname
=================

``ec2-up2date-cname`` is a utility that can update CNAME RR in route53 points to own public hostname in EC2.

Requirements
============

.. _`WebService::Amazon::Route53`: https://github.com/odyniec/WebService-Amazon-Route53
.. _`LWP`: https://github.com/gisle/libwww-perl
.. _`Tie::IxHash`: https://github.com/chorny/Tie-IxHash
.. _`XML::Simple`: http://search.cpan.org/~grantm/XML-Simple-2.18/

``ec2-up2date-cname`` is written in Perl and aims to work with RHEL 5.x based distros.

- Perl 5.8.x
- `WebService::Amazon::Route53`_

  - LWP
  - Tie::IxHash
  - XML::Simple

Install
=======

Some perl modules can be installed with yum. ::

    # yum install perl-libwww-perl perl-Crypto-SSLeay perl-XML-Simple

Tie::IxHash, WebService::Amazon::Route53 can be installed manually.

Configuration
=============

.. _`user-data`: http://docs.amazonwebservices.com/AWSEC2/latest/UserGuide/AESDG-chapter-instancedata.html#instancedata-data-retrieval

You have to create a dedicated IAM user that can access only Route53.

- `Automated DNS for AWS instances using Route 53 <http://cantina.co/2012/01/25/automated-dns-for-aws-instances-using-route-53/>`_

DO NOT PUT YOUR ACCESS KEY/SECRET KEY IN USER-DATA/INSTANCES.

``ec2-up2date-cname`` retrieves hostname points to public hostname, EC2_ACCESS_KEY,
EC2_SECRET_KEY from `user-data`_. user-data must be passed with following format::

    ${HOSTNAME}
    ${EC2_ACCESS_KEY}
    ${EC2_SECRET_KEY}

``ec2-up2date-cname`` uses a domain name in ${HOSTNAME} as zone-name in route53.

License
=======

Author: Ken-ichi TANABE <nabeken@tknetworks.org>

This program is free software; you can redistribute it and/or modify it under the same terms as Perl itself.
