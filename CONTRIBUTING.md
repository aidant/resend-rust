# Contributing

## Running the Tests

The tests make calls to the Resend API which means that the `RESEND_API_KEY` must be set in order to
run them. 

You will notice that some of the tests are slow, there's 2 reasons for this:

1. The tests all use a shared client that implements rate-limiting to avoid getting errors from
   the server
2. There are some thread sleep statements here and there to make sure that calls that create a
   resource have been properly processed

Note that because rate limiting only works for the non`blocking` feature, if more non-async tests
are added, it might be necessary to add thread sleeps.

## Missing/New Features

Before implementing or even suggesting a new feature, make sure to check the unreleased section of
[the Changelog](./CHANGELOG.md). The reason for that is that sometimes I might implement something
but not publish it immediately to avoid flooding crates.io with new releases every time a small
change is made. Open an issue about it and I'll be sure to cut a release!
