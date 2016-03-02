This document describes all tests for the Bitcoin Core project, and gives testing recommendations.

### Unit tests

Developers are strongly encouraged to write unit tests for new code, and to
submit new unit tests for old code. 

Unit tests will be automatically compiled if dependencies were met in `./configure`
and tests weren't explicitly disabled.

After configuring, they can be run with `make check`.

To run the bitcoind tests manually, launch `src/test/test_bitcoin`.

To add more bitcoind tests, add `BOOST_AUTO_TEST_CASE` functions to the existing
.cpp files in the `test/` directory or add new .cpp files that
implement new BOOST_AUTO_TEST_SUITE sections.

To run the bitcoin-qt tests manually, launch `src/qt/test/test_bitcoin-qt`

To add more bitcoin-qt tests, add them to the `src/qt/test/` directory and
the `src/qt/test/test_main.cpp` file.

### Regression and integration tests

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server. 
Once the dependencies at the previous link are installed, 
the tests can be run with: `qa/pull-tester/rpc-tests.py`

The Travis CI system makes sure that every pull request is built for Windows
and Linux, OSX, and that unit and sanity tests are automatically run.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

### Testing tips

Run with the -testnet option to run with "play bitcoins" on the test network, if you
are testing multi-machine code that needs to operate across the internet.

If you are testing something that can run on one machine, run with the -regtest option.
In regression test mode, blocks can be created on-demand; see qa/rpc-tests/ for tests
that run in -regtest mode.
