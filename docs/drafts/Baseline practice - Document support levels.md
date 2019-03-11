# Baseline practice - Document support support levels

Package maintainers provide different level of support in the large npm ecosystem.
A mismatch between the support a maintainer is planning to
provide and that expected by a consumer of a module will cause
friction and stress on both the package maintainer and
the consumer. This is further complicated because the level of support
provided for dependencies of a package may be different than that
targeted by the package a consumer is directly consuming.

This baseline practice suggests a standardized set of information to
quantify the level of support that a package maintainer wishes/is able to
provide. The goal is to close the gap between the expectations from the
consumer and those of the maintainer and reduce the friction and stress
that can arise due to the gap.

There are 4 dimensions that we standardize in this practice which are:  

* target
* response
* response-paid
* backing

For each of these dimensions the potential options are not an ordered list.
Instead like licenses each ID will identify a unique option. If you wish to
identify your package with an option which is not yet listed, please PR your
option into the lists in the sections which follow. In the package.json the values
can be any string, those which are not documented in the lists within this
document considered "custom" and may ignored for flagged by any tooling that
consumes these elements in the package.json.

In addition a `url` field can optionally be provided with a link to more detailed
support information.

The recommended baseline practice is to include an entry in `package.json`
file for a package which documents the maintainers expectations. For example:

```json
{ "support": {
    "target" : "LTS",
    "response": "BEST-EFFORT",
    "backing": "SPONSORED",
    "url": "http://mygreatmodule.org/supportinfo.html"
  }
}
```

or

```json
{ "support": {
    "target" : "LTS",
    "response": "REGULAR-7",
    "response-paid": "REGULAR-1",
    "backing": "COMPANY",
    "url": "http://mygreatmodule.org/supportinfo.html"
  }
}
```

The default for packages created by individuals for their own use should most often be:

```json
{ "support": {
    "target" : "NONE",
    "response": "BEST-EFFORT",
    "backing": "HOBBY"
  }
}
```

This reflects that the maintainer in this case may have no interest in ensuring that the package works
outside of their use case.

## Support-target

The support target captures the level of support that the package maintainer
aims to provide.  The standardized options are as follows:

* ABANDONED - Not recommended for use. The package is deprecated or no longer maintained.
* NONE - Use at your own risk, no active support. May or may not work for a given Node.js version.
* LATEST - The package is maintained only for the Latest Node.js versions. You will be required to update
  to the latest LTS Node.js version in order to ensure you can use new versions/get security fixes.
* LTS - The package is maintained for the Node.js LTS releases (both in Active and Maintenence mode).
  Anyone creating an application using an LTS version of Node.js and using the latest major version of
  LTS adopting modules will not have to accept semver-major level (ie. breaking) changes into that
  application in order to receive essential fixes.
  Full details are available in: https://github.com/nodejs/package-maintenance/issues/119
  (should we bring this into the package-maintenance repo?)
* SUPERSET - The package is maintained for versions of Node.js including both LTS and non-LTS releases. It
  may be necessary to accept semver-major level (ie. breaking) changes into that
  application in order to receive essential fixes.
  Documentation for the package will include the non-LTS releases for which the package is still maintained. 
  
  As an example based on the current active Node.js releases which are 6.x, 8.x, 10.x (LTS) and 11.x (Current)
  support would be as follows where X indicates support is provided:
  
  | Support-target| 6.x | 8.x | 10.x | 11.x | Others as documented  |
  |---------------|-----|-----|------|------|-----------------------|
  | ABANDONED     |     |     |      |      |                       |
  | NONE          |     |     |      |      |                       |
  | LATEST        |     |     |   X  |      |                       |
  | LTS           |  X  |  X  |   X  |      |                       |
  | SUPERSET      |  X  |  X  |   X  |   X  |           X           |
  
## Support-response and Support-response-paid

Support response quantifies how quickly the maintainer chooses to, or is able to, respond to issues:

* NONE - Don't expect a response, the package is not being actively maintained
* BEST-EFFORT - The maintainer is interested in fixing/discussing issues, however, there should be 
  no expectation on response times. If and when the maintainer has time they may respond.
* REGULAR-7 - There are dedicated resources who regularly maintain the module, expected response time is 7 days or less for
  a "we read your issue" response. Further work will depend on prioritization of the issue by the maintainer team.
* REGULAR-1 - There are dedicated resources who regularly maintain the module, expected response time is 1 days or less for
  a "we read your issue" response. Further work will depend on prioritization of the issue by the maintainer team.
* 24-7 - There are dedicated resources who regularly maintain the module and they are available 24/7. You can expect to 
  be able to contact the maintainers and get an initial response with 6 hours.
   
 Support-response indicates the expectation unless you have paid one of the maintainers or a company that provides
 3rd party support. If paid support is available then Support-response-paid is an array of one or more options listing the
 options that the maintainer knows are available.
 
 ## Support-backing
 
 This section can be a single value or an array of values, for example: [x, y,z]. This supports cases where the
 backing comes from more than one source. The documented options include:
 
 * NONE - There is nobody backing this module
 * HOBBY - The single maintainer maintains the package for fun, does not get any support to continue maintenance.
 * SPONSORED - The single maintainer actively maintains the package but depends on sponsorship to be able to continue to
   maintain the package. Consider supporting this sponsorship through patreon etc.
 * BOUNTY - The package is maintained through the use of a bounty service
 * PROJECT - The package is maintained under the auspices of a larger project (ex Node.js project).
 * FOUNDATION - The package is maintained and supported under the auspices of a Foundation.
 * COMPANY - The package is maintained and supported by a corporate entity but may not be related
   to their product or service offerings.
 * COMMERCIAL - The package is maintained and supported by a corporate entity as part of supporting their products.
 * PAID-SUPPORT - The package is maintained and supported through paid support contracts.
 * FREEMIUM - Basic version of the package it provided for free, premium version is available at a cost.
