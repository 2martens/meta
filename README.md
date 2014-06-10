Meta
====

Welcome to the 2martens meta repository. This repository 
is used for all meta stuff around the Web Platform. This 
includes roadmaps (what features end up in what release),
marketing documents and more.

Contributing
------------

You just came from the web-platform repo and want to contribute to the
first two phases? Great. Even if you don't came from there and want to
contribute, you are right here.

Just head over to the CONTRIBUTING.md file for detailed information.

Issues
------

The issue system of this repository will be used to ask
for features in a non-technical way. It can also contain
requests to use a specific bundle, etc. Each such request
can either be approved or declined by the Core team.

If a feature request is approved, it will be added to the
general list for planned features. Once a request is approved
and even before all contributors are invited to think about
the possible structure of that feature (one bundle, several
bundles, addition to existing bundle(s)).

Once the specific structure is set and therefore the scope
of the added bundles (if any), a corresponding issue in the
web-platform repository will be added for each bundle. This
issue describes detailed what the obligations of the bundle
are and what API it has to offer (in general terms, not specific
classes or methods).

It is then up to the contributors to develop this bundle with
the given specification. As soon as possible the developer(s)
of this bundle should add a comment to the issue stating the
concrete API, so that other developers can already start programming
against the new API.

If multiple people are working on the bundle, one person should
fork the repository, add all co-workers add contributors so that
they can develop together in a feature branch and create one
pull request for the whole bundle instead of multiple PRs with
the possibility of merge issues.
