FMS Treasury Statement Parser
-----
This uses documentation-driven development; not all of this is implemented.

Load the `./archive` submodule; this repository saves the downloaded files

    git submodule init
    git submodule update

Activate the environment

    . activate

This provides `download`, `parse` and `test` functions.

    # Download today's file
    download $(date)

After you download, you might want to commit the submodule

    cd archive
    git add .
    git commit . -m downloaded\ a\ file
    git push
    cd ..
    git commit archive -m downloaded\ a\ file

The downloaded file gets saved in `./archive`.

Run the simple parser that just gets total withdrawals, total deposits and
net change

    parse-simple

Try the complete parser that doesn't work yet.

    parse ./archive/$filename

The tests expect fixtures to be in `./fixtures`.

    test

The `run` script does all of the downloading and parsing.

    run


CSV schems
--------

Parser just for Table II for now, in two sections: Deposits and Withdrawals

For Deposits:

- Take each line item inder "Federal Reserve Account" and write to separate line with Subitem column blank, except for: 
    - Deposits by States
    - Other Deposits
    For each of these, set Item = the main line item (Deposits by States, Other Deposits)
    Then set populate column Subitem with the indented line items that roll up into the item:
- Set isTotal = 0 for all line items except:
    - Total Other Deposits
    - Total Federal Reserve Account
    - Total Deposits (excluding transfers)
    Set isTotal = 1 to flag these items as subtotals of the other items
    Keep type as Deposit for all items 






An email
----
Hope the soundsystem is blaring without me . . . stuck in the office on deadline for the banks project so unfortunately won't be able to make it tonight. 

Anyway, just wanted to pass along the scraping prototype I've created (also uploaded in our Dropbox folder), so you guys can discuss if you want. 

Open to suggestions obviously on how to structure it differently, but I think it we get a scraper to pick out the data from the text file in this or a similar 
format, we'll get pretty much everything we need off of the deposits and withdrawals tables.

I will work on a prototype for the debt tables next, which should be even simpler than this.

And will scrape the FMS directory for all the text files so we have them handy in one place. 

Anyhow, have a look and maybe we can get together on the weekend or sometime next week to push ahead with the scraping.

Take care,

Cezary


On Fri, Nov 30, 2012 at 3:21 PM, Cezary Podkul wrote:

    Gents,

    I haven't had a chance go create that CSV yet so Tom it's probably best if you go to your toilet thing tomorrow.

    Should have it done by Tuesday night so we can pick things up again then. Mike just save the code from this week and we can hook up the scraped code to SQL 
lite and copare against the CSV output then.

    Have a good weekend!

    Cezary




    On Wed, Nov 28, 2012 at 12:14 AM, Thomas Levine wrote:

        Here are the steps I plan for the parsing bit. This is the order
        that I would do them in, but if either of you are up for starting
        before our party, start with step 1 or step 4.

        1. Someone(s) manually converts one source file to eight csv files
            (one per table).
        2. Someone (probably me) writes code to load those csv files into a sqlite
            database. This is really simple; it's just the schema and
            some flags for the sqlite3 command.
        3. Someone (probably me) writes code to run SQL on two different
            databases and compare the result.
        4. Someone writes tests using the above SQL thingy. Write SQL
            queries to be run on the dataset for one table or one day. The
            result should be the same regardless of whether we run them on
            the manually parsed data or the automatically parsed data.

        After that, we write the parser, and the parser saves the data to
        an SQLite database. We use the above tests for writing the parser.


        On 2012-11-27 21:19, Cezary Podkul wrote:

            Here is the directory:

            http://www.fms.treas.gov/dts/index.html [1]


            And here is what the text files look like:


            https://www.fms.treas.gov/fmsweb/viewDTSFiles?dir=w&fname=12112600.txt
            [2]

            This might help:

            http://www.ruby-forum.com/topic/184294#805303 [3]


            Lots of great stories to be done with it!

            If we scrape it we can do them!


