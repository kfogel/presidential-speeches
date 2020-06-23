Presidential Speeches
=====================

This repository holds the raw text of over a thousand U.S.
Presidential speeches.  I think doing comparative linguistic analysis
on them might be interesting.  However, I haven't gotten around to
that part yet, so the main thing of interest here is the data -- the
speeches themselves.  There is a small amount of open source code for
doing some rudimentary analysis, but I hope someone will take this
further than I've had time to.  "Patches welcome", as the saying goes.

So far, all the texts come from [The Miller
Center](https://millercenter.org/the-presidency/presidential-speeches)
at the University of Virginia.  The Miller Center provides not just
the text of the speeches, but audio and video when available.  Since
each speech is encapsulated in a single web page and those pages are
in a pretty consistent format (thank you, Miller Center!), the raw
text for each speech was easily extractable.  I used
[Emacs](https://www.gnu.org/software/emacs/) macros (thank you,
Emacs!), but one could easily script the process in any programming
language.  See the section "Notes on data formatting and consistency"
below for details.

Comparative analysis.
---------------------

Work in progress; start by running [do-all](do-all).

Notes on data formatting and consistency.
-----------------------------------------

Each transcript in the [data](data) directory starts with a single
line of the form "President: Name Of Some President", followed after a
blank line by the transcript.

The presidential identifiers appear to be consistent, e.g., LBJ is
always "Lyndon B. Johnson", never "Lyndon Johnson".  Here's how I
checked:

            $ grep -h "^President: " data/* | sort | uniq
            President: Abraham Lincoln
            President: Andrew Jackson
            President: Andrew Johnson
            President: Barack Obama
            President: Benjamin Harrison
            President: Bill Clinton
            President: Calvin Coolidge
            President: Chester A. Arthur
            President: Donald Trump
            President: Dwight D. Eisenhower
            President: Franklin D. Roosevelt
            President: Franklin Pierce
            President: George H. W. Bush
            President: George Washington
            President: George W. Bush
            President: Gerald Ford
            President: Grover Cleveland
            President: Harry S. Truman
            President: Herbert Hoover
            President: James A. Garfield
            President: James Buchanan
            President: James K. Polk
            President: James Madison
            President: James Monroe
            President: Jimmy Carter
            President: John Adams
            President: John F. Kennedy
            President: John Quincy Adams
            President: John Tyler
            President: Lyndon B. Johnson
            President: Martin Van Buren
            President: Millard Fillmore
            President: Richard Nixon
            President: Ronald Reagan
            President: Rutherford B. Hayes
            President: Theodore Roosevelt
            President: Thomas Jefferson
            President: Ulysses S. Grant
            President: Warren G. Harding
            President: William Harrison
            President: William McKinley
            President: William Taft
            President: Woodrow Wilson
            President: Zachary Taylor
            $ 

Each data file's name can be algorithmically transformed back to its
original URL:

1. Convert the file's "YYYY-MM-DD" prefix to "monthname-D-YYYY".  For
   example, "2008-11-04" would become "november-4-2008".

2. Strip off the `.txt` from the end of the filename.

3. Prepend `https://millercenter.org/the-presidency/presidential-speeches/`.

For example,

      data/2013-01-21-second-inaugural-address.txt

corresponds to this URL:

      https://millercenter.org/the-presidency/presidential-speeches/january-21-2013-second-inaugural-address

Below is a list of various consistency and formatting issues I have
noticed in the data.  Some of these are issues that would likely
affect any comparative analysis and thus would have to be filtered out
or otherwise handled specially.  A general solution would be a 'pcat'
command ("presidential catenate", like Unix 'cat' but living in the
White House I guess) that takes a transcript as input and prints just
the President's actual words as output.

* Double hyphen used for em-dash is inconsistently spaced.

  In some speeches--particularly the older ones--the double hyphen
  without spaces on either side is used em-dash, as in this sentence.
  In other speeches -- particularly the newer ones -- it's done with
  spaces on either side, as in this sentence.

* Debates and press conferences include other speakers.

  Many of these transcripts are not speeches but rather debates or
  press conferences, in which other speakers' words are included.  For
  debates, the moderator and other participants are included, and this
  can be a significant amount of the text.  For press conferences,
  when it's just the President answering questions from reporters,
  most of the words are President's with a few words from reporters,
  but when it is a joint press conference with another politician,
  e.g., data/1991-07-31-press-conference-mikhail-gorbachev.txt, then
  a lot of the words in the file are from sources other than the
  President.

          $ ls data/*conference*
          data/1890-04-19-statement-international-american-conference.txt
          data/1921-11-12-opening-speech-conference-limitation-armament.txt
          data/1943-12-24-fireside-chat-27-tehran-and-cairo-conferences.txt
          data/1945-08-09-radio-report-american-people-potsdam-conference.txt
          data/1964-02-01-press-conference.txt
          data/1964-02-29-press-conference-state-department.txt
          data/1964-03-07-press-conference-white-house.txt
          data/1964-04-16-press-conference-state-department.txt
          data/1964-05-06-press-conference-south-lawn.txt
          data/1964-07-24-press-conference-state-department.txt
          data/1965-02-04-press-conference.txt
          data/1965-03-13-press-conference-white-house.txt
          data/1965-03-20-press-conference-lbj-ranch.txt
          data/1965-04-27-press-conference-east-room.txt
          data/1965-06-01-press-conference-east-room.txt
          data/1965-07-13-press-conference-east-room.txt
          data/1965-07-28-press-conference.txt
          data/1965-08-25-press-conference-white-house.txt
          data/1966-07-05-press-conference-lbj-ranch.txt
          data/1966-07-20-press-conference-east-room.txt
          data/1966-10-06-press-conference.txt
          data/1966-12-31-press-conference.txt
          data/1967-02-02-press-conference.txt
          data/1967-03-09-press-conference.txt
          data/1967-08-18-press-conference.txt
          data/1967-11-17-press-conference.txt
          data/1968-04-03-press-conference.txt
          data/1974-02-25-presidents-news-conference.txt
          data/1977-03-09-remarks-president-carters-press-conference.txt
          data/1981-01-29-first-press-conference.txt
          data/1991-07-31-press-conference-mikhail-gorbachev.txt
          data/1993-01-29-press-conference-gays-military.txt
          data/2009-01-12-final-press-conference.txt
          data/2010-02-09-news-conference-congressional-gridlock.txt
          data/2010-11-03-press-conference-after-2010-midterm-elections.txt
          $ ls data/*debate*
          data/1960-09-26-debate-richard-nixon-chicago.txt
          data/1960-10-07-debate-richard-nixon-washington-dc.txt
          data/1960-10-13-debate-richard-nixon-new-york-and-los-angeles.txt
          data/1960-10-21-debate-richard-nixon-new-york.txt
          data/1976-09-23-debate-president-gerald-ford-domestic-issues.txt
          data/1976-10-06-debate-president-gerald-ford-foreign-and.txt
          data/1976-10-22-debate-president-gerald-ford.txt
          data/1980-10-28-debate-ronald-reagan.txt
          data/1984-10-07-debate-walter-mondale-domestic-issues.txt
          data/1984-10-21-debate-walter-mondale-defense-and-foreign.txt
          data/1988-09-25-debate-michael-dukakis.txt
          data/1992-10-11-debate-bill-clinton-and-ross-perot.txt
          data/1996-10-06-presidential-debate-senator-bob-dole.txt

* One speech was missing the presidential identifier element.

  [This](data/2011-09-08-address-congress-american-jobs-act.txt)
  speech, given by Barack Obama on 8 Sep 2011, was missing a
  standardized HTML element that every other speech uses to identify
  the president who gave the speech.  I added the element...

          <p class="president-name">Barack Obama</p>

  ...right before the line indicating the date of the speech, which
  was present here expected:
 
          <p class="episode-date">September 08, 2011</p>

  I reported this 2017-05-14 via https://millercenter.org/contact.

* 19 speeches are missing the HTML element that indicates location.

  We don't include location information in the raw transcripts in the
  [data](data) directory, since our analyses don't take location into
  account anyway, but FWIW 19 of the speeches as downloaded from the
  Miller Center didn't have the `'<span class="speech-loc">...</span>'` 
  element in their HTML.  The command below won't work anymore, since
  we later stripped out all the location data, but at the time it
  showed which speeches were missing location information:

          $ for name in *;                                        \
              do if grep -q '<span class="speech-loc">' ${name};  \
                    then echo -n ""; else echo "${name}";         \
                 fi;                                              \
              done
          1842-08-11-message-senate-negotiations-britain.txt
          1965-01-20-inaugural-address.txt
          1981-04-28-address-program-economic-recovery.txt
          1981-11-18-speech-strategic-arms-reduction-talks.txt
          1982-06-09-address-bundestag-west-germany.txt
          1982-06-17-speech-united-nations-general-assembly.txt
          1982-09-20-address-nation-lebanon.txt
          1983-03-23-address-nation-national-security.txt
          1983-11-02-speech-creation-martin-luther-king-jr-national.txt
          1983-11-04-remarks-us-casualties-lebanon-and-grenada.txt
          1984-06-06-40th-anniversary-d-day.txt
          1984-10-07-debate-walter-mondale-domestic-issues.txt
          1985-05-05-bergen-belsen-concentration-camp.txt
          1986-09-14-speech-nation-campaign-against-drug-abuse.txt
          1988-08-15-farewell-address-republican-national-convention.txt
          1988-12-16-speech-foreign-policy.txt
          2004-07-17-remarks-national-security-and-war-effort.txt
          2011-05-19-speech-american-diplomacy-middle-east-and-north.txt
          2011-10-21-remarks-end-war-iraq.txt
          $ 

  This element is normally present in the Miller Center web page for
  each speech, and looks something like this:

          <span class="speech-loc">The White House</span>

  In most or all of the speeches where it's missing, the location is
  known.  E.g., we clearly know where Ronald Reagan's [1982 speech at
  the Bundestag](1982-06-09-address-bundestag-west-germany.txt) took
  place.

  This issue is also mentioned in my 2017-05-14 report to
  https://millercenter.org/contact.

* The transcript of at least one speech is really a summary.

  The transcript of [this
  speech](data/1841-02-24-argument-supreme-court-case-united-states-v.txt)
  is really a summary (see original at
  https://millercenter.org/the-presidency/presidential-speeches/february-24-1841-argument-supreme-court-case-united-states-v).

  How many more such are there?  I don't know yet.

* Unexpected number and spelling in one speech.  

  [This speech](data/1793-03-04-second-inaugural-address) has the
  number "56" inline in the text, and spells a word "punishmt".  Are
  there other old speeches with odd spelling?

  How many other transcripts have issues like that?  I don't know yet.

* Some speeches were actually written out and signed.
  The say "By the president" or some such at the bottom, and
  often mention another official who facilitated the transmission.
  See, e.g., [this
  one](data/1869-05-19-proclamation-establishing-eight-hour-workday.txt).
  Others are signed "Very respectfully," or some such, e.g., [this
  one](data/1877-06-22-prohibition-federal-employees-political.txt).

  At the very least, such footer text should be stripped for the
  purposes of textual analysis, because it's not part of what the
  President said.
