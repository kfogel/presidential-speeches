Presidential Speeches
=====================

This repository holds the raw text of 978 presidential speeches, and
some open source code for doing (so far rudimentary) analysis of them.

The texts come from [The Miller
Center](https://millercenter.org/the-presidency/presidential-speeches)
at the University of Virginia.  The Miller Center provides not just
the text of the speeches, but audio and video when available.
However, since each speech is encapsulated in a single web page and
those pages are in a pretty consistent format (thank you, Miller
Center!), the raw text for each speech was easily extractable via
[Emacs](https://www.gnu.org/software/emacs/) macros.  See the section
"Notes on data formatting and consistency" below for details.

As of this writing, the code isn't here yet.  It's coming soon :-).

Notes on data formatting and consistency.
-----------------------------------------

Each transcript in the [data](data) directory starts with a single
line of the form "President: Name Of Some President", followed on
the next line (or maybe after some blank lines) by the transcript.

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
original URL.  Just strip off the `.txt` from the end, and prepend
`https://millercenter.org/the-presidency/presidential-speeches/`.

* Debates and press conferences include other speakers.

  Many of these transcripts are not speeches but rather debates or
  press conferences, in which other speakers' words are included.  For
  debates, the moderator and other participants are included, and this
  can be a significant amount of the text.  For press conferences,
  when it's just the President answering questions from reporters,
  most of the words are President's with a few words from reporters,
  but when it is a joint press conference with another politician,
  e.g., data/july-31-1991-press-conference-mikhail-gorbachev.txt, then
  a lot of the words in the file are from sources other than the
  President.

          $ ls data/*conference*
          data/april-16-1964-press-conference-state-department.txt
          data/april-19-1890-statement-international-american-conference.txt
          data/april-27-1965-press-conference-east-room.txt
          data/april-3-1968-press-conference.txt
          data/august-18-1967-press-conference.txt
          data/august-25-1965-press-conference-white-house.txt
          data/august-9-1945-radio-report-american-people-potsdam-conference.txt
          data/december-24-1943-fireside-chat-27-tehran-and-cairo-conferences.txt
          data/december-31-1966-press-conference.txt
          data/february-1-1964-press-conference.txt
          data/february-2-1967-press-conference.txt
          data/february-25-1974-presidents-news-conference.txt
          data/february-29-1964-press-conference-state-department.txt
          data/february-4-1965-press-conference.txt
          data/february-9-2010-news-conference-congressional-gridlock.txt
          data/january-12-2009-final-press-conference.txt
          data/january-29-1981-first-press-conference.txt
          data/january-29-1993-press-conference-gays-military.txt
          data/july-13-1965-press-conference-east-room.txt
          data/july-20-1966-press-conference-east-room.txt
          data/july-24-1964-press-conference-state-department.txt
          data/july-28-1965-press-conference.txt
          data/july-31-1991-press-conference-mikhail-gorbachev.txt
          data/july-5-1966-press-conference-lbj-ranch.txt
          data/june-1-1965-press-conference-east-room.txt
          data/march-13-1965-press-conference-white-house.txt
          data/march-20-1965-press-conference-lbj-ranch.txt
          data/march-7-1964-press-conference-white-house.txt
          data/march-9-1967-press-conference.txt
          data/march-9-1977-remarks-president-carters-press-conference.txt
          data/may-6-1964-press-conference-south-lawn.txt
          data/november-12-1921-opening-speech-conference-limitation-armament.txt
          data/november-17-1967-press-conference.txt
          data/november-3-2010-press-conference-after-2010-midterm-elections.txt
          data/october-6-1966-press-conference.txt
          $ ls data/*debate*
          data/october-11-1992-debate-bill-clinton-and-ross-perot.txt
          data/october-13-1960-debate-richard-nixon-new-york-and-los-angeles.txt
          data/october-21-1960-debate-richard-nixon-new-york.txt
          data/october-21-1984-debate-walter-mondale-defense-and-foreign.txt
          data/october-22-1976-debate-president-gerald-ford.txt
          data/october-28-1980-debate-ronald-reagan.txt
          data/october-6-1976-debate-president-gerald-ford-foreign-and.txt
          data/october-6-1996-presidential-debate-senator-bob-dole.txt
          data/october-7-1960-debate-richard-nixon-washington-dc.txt
          data/october-7-1984-debate-walter-mondale-domestic-issues.txt
          data/september-23-1976-debate-president-gerald-ford-domestic-issues.txt
          data/september-25-1988-debate-michael-dukakis.txt
          data/september-26-1960-debate-richard-nixon-chicago.txt

* One speech was missing the presidential identifier element.

  [This](data/september-8-2011-address-congress-american-jobs-act.txt)
  speech, given by Barack Obama on 8 Sep 2011, was missing a
  standardized HTML element that every other speech uses to identify
  the president who gave the speech.  I added the element...

          <p class="president-name">Barack Obama</p>

  ...right before the line indicating the date of the speech, which
  was present here expected:
 
          <p class="episode-date">September 08, 2011</p>

  I reported this 2017-05-14 via https://millercenter.org/contact.

* 19 speeches are missing the HTML element that indicates location.

  I haven't added this element, since none of the analysis I'm doing
  takes location into account, but FWIW 19 speeches (about 2%) were
  missing the `'<span class="speech-loc">...</span>'` element:

          $ for name in *;                                        \
              do if grep -q '<span class="speech-loc">' ${name};  \
                    then echo -n ""; else echo "${name}";         \
                 fi;                                              \
              done
          april-28-1981-address-program-economic-recovery
          august-11-1842-message-senate-negotiations-britain
          august-15-1988-farewell-address-republican-national-convention
          december-16-1988-speech-foreign-policy
          january-20-1965-inaugural-address
          july-17-2004-remarks-national-security-and-war-effort
          june-17-1982-speech-united-nations-general-assembly
          june-6-1984-40th-anniversary-d-day
          june-9-1982-address-bundestag-west-germany
          march-23-1983-address-nation-national-security
          may-19-2011-speech-american-diplomacy-middle-east-and-north
          may-5-1985-bergen-belsen-concentration-camp
          november-18-1981-speech-strategic-arms-reduction-talks
          november-2-1983-speech-creation-martin-luther-king-jr-national
          november-4-1983-remarks-us-casualties-lebanon-and-grenada
          october-21-2011-remarks-end-war-iraq
          october-7-1984-debate-walter-mondale-domestic-issues
          september-14-1986-speech-nation-campaign-against-drug-abuse
          september-20-1982-address-nation-lebanon
          $ 

  This element is normally present in the Miller Center web page for
  each speech, and looks something like this:

          <span class="speech-loc">The White House</span>

  In most or all of the speeches where it's missing, the location is
  known.  E.g., we clearly know where Ronald Reagan's [1982 speech at
  the Bundestag](june-9-1982-address-bundestag-west-germany.txt) took
  place.

  This issue is also mentioned in my 2017-05-14 report to
  https://millercenter.org/contact.

  Note that the raw texts in the [data](data) directory do not include
  the HTML anymore, so the above will not run against current data.

* The transcript of at least one speech is really a summary.

  The transcript of [this
  speech](data/february-24-1841-argument-supreme-court-case-united-states-v.txt)
  is really a summary (see original at
  https://millercenter.org/the-presidency/presidential-speeches/february-24-1841-argument-supreme-court-case-united-states-v).

* Unexpected number and spelling in one speech.  

  [This speech](data/march-4-1793-second-inaugural-address) has the
  number "56" inline in the text, and spells a word "punishmt".  Are
  there other old speeches with odd spelling?

* Some things are really written out and signed.
  The say "By the president" or some such at the bottom, and
  often mention another official who facilitated the transmission.
  See, e.g., [this
  one](data/may-19-1869-proclamation-establishing-eight-hour-workday.txt).

* Some speeches are signed "Very respectfully," or some such.
  E.g., [this
  one](data/june-22-1877-prohibition-federal-employees-political.txt).
