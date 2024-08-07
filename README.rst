===============================
Python SDK for Codequiry API
===============================

Codequiry is a commercial grade plagiarism and similarity detection software for source code files. Submissions are checked with billions of sources on the web as well as checked locally against provided submissions. This is a NodeJS example application for the API to check code plagiarism and similarity.

The API allows us to run multiple different tests on source code files:

    Peer Check - Given a group of submissions as individual zip files, all lines of code are compared to each other and relative similarity scores are computed, as well as matched snippets.
    Database Check - Checks submissions against popular repositories and public sources of code.
    Web Check - Does a full check of code with over 2 billion public sources on the web.

Checks return us tons of data such as similarity scores, individual file scores, cluster graphs, similarity histograms, highlights results, matched snippets, percentage plagiarised and similar, and a ton more...

Main Website: https://codequiry.com

Full API Docs: https://codequiry.com/usage/api

Installation
------------
.. code-block:: python

    pip install -r requirements.txt

Usage
------------

Setting your API Key
--------------------
.. code:: python

    sdk = Codequiry("API_KEY")

Getting account information
---------------------------
.. code:: python

    account = sdk.account()
    print(account)

Getting checks
--------------
.. code:: python

    checks = sdk.account()
    print(checks)


Creating checks (specify name and programming language id)
-------------------------------------------------------
Examples: javascript, java, c-cpp, python, csharp, txt
.. code:: python

    check = sdk.create_check("checkname", "39")
    print(check)

Uploading to a check (specify check_id and file (must be a zip file))
---------------------------------------------------------------------

.. code:: python

    upload = sdk.upload_file(CHECK_ID, './Test.zip')
    print(upload)

Starting a check (specify check_id and if running database check or web check)
------------------------------------------------------------------------------

.. code:: python

    check = sdk.start_check(CHECK_ID)
    print(check)

Getting a check information/status
----------------------------------

.. code:: python

    check = sdk.get_check(CHECK_ID)
    print(check)

Getting results overview
------------------------

.. code:: python

    overview = sdk.overview(CHECK_ID)
    print(overview)

Getting specific results of a submission
-----------------------------------------
.. code:: python

    results = sdk.get_results(CHECK_ID, SID)
    print(results)

Realtime checking progress - SocketIO
--------------------------------------

This is an example of the listener, you can call this after getting a check status or after starting a check (both will reutrn a job ID, which you can listen to). Here we will listen to specific CHECK_ID.

.. code:: python

    def get_status(status):
        print(status)

    sdk.check_listen(CHECK_ID, get_status)
