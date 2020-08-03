Inscope Metrics Build Resources
===============================

2.1.1 - TBD
------------------------
* TBD

2.1.0 - August 2, 2020
------------------------
* Included docker-entrypoint.sh to allow runtime specification of run-as user.
* Fixed bug in app assembler Unix launch script to pass through JAVA_OPTS.

2.0.4 - May 5, 2020
------------------------
* Inner types should be last.
* Declaration order; static members, non-static members, constructors, method.
* Added rule to disallow explicitl package private declarations via comment.
* Fixed `RegexpSingleline` for `<code>...</code>` migration to `{@code ...}`.
* Moved LineLength check out of TreeWalker for compatibility as per [checkstyle#2116](https://github.com/checkstyle/checkstyle/issues/2116).

2.0.3 - July 8, 2019
------------------------
* Initial release to `io.inscopemetrics.build:build-resources`.

Published under Apache Software License 2.0, see LICENSE

&copy; Inscope Metrics, 2019
