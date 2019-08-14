W241 Final Project Essay
================
Tucker Anderson and Carlos Sancini

## Cell Phone Mindfulness Study

### Background

Cell phone, or smart phone, usage has increased dramatically in the past
few years. Ownership has become so pervasive that now 96% of Americans
own a smartphone(<https://www.pewinternet.org/fact-sheet/mobile>). This
permutation of technology has had a tremendous impact the world over.
From browsing the internet to texting your friends to playing Candy
Crush, it’s easier than ever to pull your phone out of your pocket to
respond to an email or to try and quash that split second feeling of
boredom. Software is eating the world and the mobile platform is
providing users a limitless means to disconnect. This increased
connectivity to the web has some concerned that we may be spending too
much of our time and attention in the screens of our phones

The Screen Time application developed by Apple is included by default in
all iOS 12 and greater phones. This applications automatically tracks
the time and application use of the user, and seemed to be a great way
to measure our primary dependent variable of interest: time spent using
the phone each day or each week.

### Experimental Design

We designed a set of surveys to extract a sample of the population’s use
of cell phones. We isolated a subset of the population, only reaching
out to users who owned an Apple smartphone which had iOS 12 or higher
installed, to utilize the Screen Time app and ensure our measurement
methodology was consistent between all subjects. We believed the
consistent measurement benefit would outweigh the effects of leaving out
large subsets of the population such as Android phone users. The
assumption here is that there is no fundamental difference at the
population scale between Apple smartphone users and users of other
smartphone platforms. While it seems possible that there may be some

We ran a quick power analysis to determine the required amoung of
subjects in the control and treatment group. In this test we assumed a
minimum power of 0.80, as per Cohen’s reasoning that studies should have
a maximum Type II error rate of 0.20, and a significance level of 0.05
as per the standard practice of setting alpha Type I error rates to
0.05. We worried that the effect size of “mindfulness” of screen time
could be very small

``` r
# determine sample size required to achieve a power of 80% (Tpe II error rate of 20%) and a Type I error rate of 5% with a negligible effect size
pwr.t.test(d = 0.3, sig.level = 0.05, power = 0.80)
```

    ## 
    ##      Two-sample t test power calculation 
    ## 
    ##               n = 175.3847
    ##               d = 0.3
    ##       sig.level = 0.05
    ##           power = 0.8
    ##     alternative = two.sided
    ## 
    ## NOTE: n is number in *each* group

We see based on our power calculation that, assuming our effect size
would be about 0.3, we would like to achieve a sample size of about 175
for each group, or about 350 total subjects with a perfect 50/50 split.
However, our team foresaw a large attrition bias from subjects in this
study, it’s always hard to get the same subjects to respond to a similar
survey after one and especially two weeks. Considering this, with an
expectation of a possible 25% attriton rate between weeks, we would like
to generate survey responses from 437 participants, rounding up to a
clean 500. Accounting for attrition in this way will hopefully keep our
statistical power through the weeks, but it still leaves the possible
bias of those attriting due to some inexplicable difference between the
rest of subjects. Perhaps those who attrit naturally use their phone
less or are more perceptible to our treatment. This is something to keep
in mind for our analysis.

We also had concerns about compliance; would our subjects properly read
the articles given to them? Would treatment subjects properly read their
articles? We wanted to use Qualtrics’ timing feature and link clicking

### Issues Conducting Experiment

Unfortunately, we were not able to successfully conduct our study as
specified above. Amazon’s Mechanical Turk suspended our academic and
personal accounts for PII violations (but as of 8/13/19 still have not
provided what part of the survey questions were deemed to be in
violation) and non-American account statuses. Attempting to
reconsolidate these issues took weeks off of our schedule and eventually
only allowed us to collect partial baseline data three times. In light
of this, no true treatment (re-surveying after patients read an article
about the benefits of mindfulness of cell phone use) was administered
and no effect from our original design can be extracted.

### Data Analysis

``` r
# ingest data into a data table
d <- fread('./data/phone_data.csv')

d.size <- dim(d)
```

We ended up with 967 baseline records with a number of useful covariates
such as gender, blue collar vs white collar, and our dependent variable
of interest screen time from the app.

### EDA

Let’s quickly explore our baseline data.

    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.00320435,-117.9617004&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   William Steinmetz Park, 1545 S Stimson Ave, Hacienda Heights, CA 91745, USA
    ##   1545 S Stimson Ave, Hacienda Heights, CA 91745, USA
    ##   15906 Three Palms St, Hacienda Heights, CA 91745, USA
    ##   Unnamed Road, Hacienda Heights, CA 91745, USA
    ##   Hacienda Heights, CA, USA
    ##   Hacienda Heights, CA 91745, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.38250732,-79.2181015&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1104 McConville Rd, Lynchburg, VA 24502, USA
    ##   1131 McConville Rd, Lynchburg, VA 24502, USA
    ##   1273-1137 McConville Rd, Lynchburg, VA 24502, USA
    ##   Lynchburg, VA 24502, USA
    ##   Lynchburg, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.73899841,-84.08560181&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1625 Ken Klare Dr, Dayton, OH 45432, USA
    ##   1616 Brook Lynn Dr, Beavercreek, OH 45432, USA
    ##   1626 Ken Klare Dr, Beavercreek, OH 45432, USA
    ##   1689-1637 Brook Lynn Dr, Beavercreek, OH 45432, USA
    ##   Dayton, OH 45432, USA
    ##   Beavercreek, OH, USA
    ##   Beavercreek Township, OH, USA
    ##   Greene County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.89289856,-80.04579926&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Graves Dr, Joint Base Charleston, SC 29404, USA
    ##   Charleston International Airport (CHS), 5500 International Blvd, North Charleston, SC 29418, USA
    ##   Joint Base Charleston, SC 29404, USA
    ##   North Charleston, SC, USA
    ##   Charleston County, SC, USA
    ##   South Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.76139832,-78.60150146&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1500 Rose Ln, Raleigh, NC 27610, USA
    ##   Dacian Road Park, 566 Dacian Rd, Raleigh, NC 27610, USA
    ##   570 Rose Ln, Raleigh, NC 27610, USA
    ##   Walnut Creek Trail, Raleigh, NC 27610, USA
    ##   570 Dacian Rd, Raleigh, NC 27610, USA
    ##   Southeast Raleigh, Raleigh, NC, USA
    ##   Raleigh, NC, USA
    ##   Raleigh, NC 27610, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.33880615,-97.53230286&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   12608 Bella Pkwy, Manor, TX 78653, USA
    ##   12691 Old Hwy 20, Manor, TX 78653, USA
    ##   Bella Pkwy, Manor, TX 78653, USA
    ##   Webberville, TX 78653, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.73730469,-95.39720154&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Menil Park, 1423 Branard St, Houston, TX 77006, USA
    ##   1417 Sul Ross St, Houston, TX 77006, USA
    ##   3956 Mulberry St, Houston, TX 77006, USA
    ##   1599-1461 Branard St, Houston, TX 77006, USA
    ##   Houston, TX 77006, USA
    ##   Montrose, Houston, TX, USA
    ##   Houston, TX, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.01179504,-73.86650085&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   120 Bellewood Ave, Dobbs Ferry, NY 10522, USA
    ##   120 Walgrove Ave, Dobbs Ferry, NY 10522, USA
    ##   117 Walgrove Ave, Dobbs Ferry, NY 10522, USA
    ##   72-198 Bellewood Ave, Dobbs Ferry, NY 10522, USA
    ##   Dobbs Ferry, NY, USA
    ##   Dobbs Ferry, NY 10522, USA
    ##   Greenburgh, NY, USA
    ##   Westchester County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.76879883,-122.262001&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1432 San Antonio Ave, Alameda, CA 94501, USA
    ##   1025 Morton St, Alameda, CA 94501, USA
    ##   974 Morton St, Alameda, CA 94501, USA
    ##   1300-1398 San Antonio Ave, Alameda, CA 94501, USA
    ##   West Alameda, Alameda, CA 94501, USA
    ##   Alameda, CA 94501, USA
    ##   Alameda, CA, USA
    ##   Alameda County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=10.99099731,76.96670532&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   94, Vincent Rd, Fort, Coimbatore, Tamil Nadu 641001, India
    ##   Vincent Rd, Ukkadam, Coimbatore, Tamil Nadu 641008, India
    ##   Ukkadam, Coimbatore, Tamil Nadu 641001, India
    ##   Coimbatore, Tamil Nadu 641001, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.70089722,-73.94609833&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Bartlett Playground, 5002, 11 Whipple St, Brooklyn, NY 11206, United States
    ##   38 Bartlett St, Brooklyn, NY 11206, USA
    ##   51 Bartlett St, Brooklyn, NY 11206, USA
    ##   Broadway Triangle, Brooklyn, NY 11206, USA
    ##   Brooklyn, NY 11206, USA
    ##   Brooklyn, NY, USA
    ##   Kings County, Brooklyn, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=55.18080139,-118.9103012&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Township Rd 715, Grande Prairie, AB T8V 7Z8, Canada
    ##   Grande Prairie, AB T8V 7Z8, Canada
    ##   Grande Prairie, AB T8V, Canada
    ##   Grande Prairie, AB, Canada
    ##   Division No. 19, AB, Canada
    ##   Alberta, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-23.60710144,-46.30999756&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road - Jardim Nova America, Suzano - SP, Brazil
    ##   Jardim Nova America, Suzano - SP, Brazil
    ##   Suzano - State of São Paulo, Brazil
    ##   Suzano - Palmeiras de São Paulo, Suzano - State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.51150513,-98.97949982&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   315 S 16th St, Clinton, OK 73601, USA
    ##   305 S 16th St, Clinton, OK 73601, USA
    ##   322 S 15th St, Clinton, OK 73601, USA
    ##   318 S 16th St, Clinton, OK 73601, USA
    ##   200-298 S 16th St, Clinton, OK 73601, USA
    ##   Clinton, OK, USA
    ##   Clinton, OK 73601, USA
    ##   Custer County, OK, USA
    ##   Oklahoma, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.72410583,-88.93009949&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1018 S Holland St, Marion, IL 62959, USA
    ##   1008 S Monroe St, Marion, IL 62959, USA
    ##   1050 S Holland St, Marion, IL 62959, USA
    ##   Gent St, Marion, IL 62959, USA
    ##   Marion, IL, USA
    ##   West Marion Precinct, IL, USA
    ##   Marion, IL 62959, USA
    ##   Williamson County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.07150269,-76.69629669&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   601 Chapelgate Dr, Odenton, MD 21113, USA
    ##   603 Chapelgate Dr, Odenton, MD 21113, USA
    ##   623-601 Chapelgate Dr, Odenton, MD 21113, USA
    ##   Odenton, MD, USA
    ##   Odenton, MD 21113, USA
    ##   Hanover, MD, USA
    ##   Anne Arundel County, MD, USA
    ##   Maryland, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.96090698,-77.34290314&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1711 Clubhouse Rd, Reston, VA 20190, USA
    ##   The Blue Trail, Reston, VA 20190, USA
    ##   Herndon, VA 20190, USA
    ##   Reston, VA, USA
    ##   Hunter Mill, VA, USA
    ##   Fairfax County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.53770447,-105.0546036&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1317 E Horsetooth Rd, Fort Collins, CO 80525, USA
    ##   Warren Park, 1061 Driftwood Dr, Fort Collins, CO 80525, USA
    ##   E Horsetooth Rd, Fort Collins, CO 80525, USA
    ##   The Landings, Fort Collins, CO 80525, USA
    ##   Fort Collins, CO 80525, USA
    ##   Fort Collins, CO, USA
    ##   Larimer County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.76519775,-73.95880127&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   St. Catherine's Park, 1245 1st Avenue, New York, NY 10065, USA
    ##   1245 1st Avenue, New York, NY 10065, USA
    ##   E 67 St & 1 Av, New York, NY 10065, USA
    ##   361 E 67th St, New York, NY 10065, USA
    ##   New York, NY 10065, USA
    ##   Lenox Hill, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=13.08430481,80.28048706&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Esplanade, Park Town, Chennai, Tamil Nadu 600003, India
    ##   Esplanade, George Town, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600003, India
    ##   Park Town, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.85450745,-96.59909821&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5100 Broadway Blvd, Garland, TX 75043, USA
    ##   Broadway @ Palo Alto - N - NS, Garland, TX 75043, USA
    ##   5075 Branch Hollow Dr, Garland, TX 75043, USA
    ##   Garland, TX 75043, USA
    ##   Garland, TX, USA
    ##   Dallas County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.29570007,-76.62889862&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   907 Myrtle Ave, Baltimore, MD 21201, USA
    ##   623 George St, Baltimore, MD 21201, USA
    ##   904 Myrtle Ave, Baltimore, MD 21201, USA
    ##   Myrtle Ave, Baltimore, MD 21201, USA
    ##   Heritage Crossing, Baltimore, MD 21201, USA
    ##   Baltimore, MD 21201, USA
    ##   Baltimore, MD, USA
    ##   Maryland, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=13.08459473,80.24841309&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.88679504,-87.63860321&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   165 NW Water St, Chicago, IL 60606, USA
    ##   Chicago, IL 60606, USA
    ##   Fulton River District, Chicago, IL, USA
    ##   Chicago, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.7467041,-74.05740356&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3359 John F. Kennedy Blvd, Union City, NJ 07087, USA
    ##   JFK Blvd at Hutton St, Jersey City, NJ 07307, USA
    ##   3340 John F. Kennedy Blvd, Jersey City, NJ 07307, USA
    ##   3363-3359 John F. Kennedy Blvd, Jersey City, NJ 07307, USA
    ##   The Heights, Jersey City, NJ, USA
    ##   Jersey City, NJ 07307, USA
    ##   Jersey City, NJ, USA
    ##   Hudson County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=51.5164032,-0.093002319&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10 Aldermanbury, London EC2V 7RF, UK
    ##   1 Love Ln, London EC2V, UK
    ##   Aldermanbury, London EC2V, UK
    ##   Love Ln, London EC2V 7JN, UK
    ##   London EC2V, UK
    ##   City of London, UK
    ##   City of London, London, UK
    ##   London, UK
    ##   Greater London, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.73350525,-79.41770172&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   195 Brooke Ave, North York, ON M5M 2K7, Canada
    ##   197 Brooke Ave, North York, ON M5M 2K7, Canada
    ##   North York, ON M5M 2K7, Canada
    ##   Bedford Park, Toronto, ON, Canada
    ##   Toronto, ON M5M, Canada
    ##   Old Toronto, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=11.00549316,76.96609497&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-12.86650085,-38.48579407&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Tv. Eng. Agenor de Freitas de Periperi, 2 - Periperi, Salvador - BA, 40720-401, Brazil
    ##   Tv. Eng. Agenor de Freitas de Periperi, 61-1 - Periperi, Salvador - BA, 40720-401, Brazil
    ##   Salvador - State of Bahia, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.05439758,-118.2440033&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   205 N Spring St, Los Angeles, CA 90012, USA
    ##   227 N Spring St, Los Angeles, CA 90012, USA
    ##   233 N Spring St, Los Angeles, CA 90012, USA
    ##   Unnamed Road, Los Angeles, CA 90012, USA
    ##   Little Tokyo, Los Angeles, CA, USA
    ##   Los Angeles, CA 90012, USA
    ##   Downtown Los Angeles, Los Angeles, CA, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.33799744,-111.7434998&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   671 S Columbus Dr, Gilbert, AZ 85296, USA
    ##   Finley Farms South Tot Lot Park, 671 S Columbus Dr, Gilbert, AZ 85296, USA
    ##   2199 E Catclaw St, Gilbert, AZ 85296, USA
    ##   628-668 S Columbus Dr, Gilbert, AZ 85296, USA
    ##   Finley Farms South, Gilbert, AZ 85296, USA
    ##   Gilbert, AZ 85296, USA
    ##   Gilbert, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.57800293,-116.2953949&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2837 S Maple Grove Rd, Boise, ID 83709, USA
    ##   Molenaar Park, 2815 S Maple Grove Rd, Boise, ID 83709, USA
    ##   2815 S Maple Grove Rd, Boise, ID 83709, USA
    ##   2768 S Maple Grove Rd, Boise, ID 83709, USA
    ##   2485-2743 S Maple Grove Rd, Boise, ID 83709, USA
    ##   Southwest Ada County Alliance, Boise, ID 83709, USA
    ##   Boise, ID 83709, USA
    ##   Boise, ID, USA
    ##   Ada County, ID, USA
    ##   Idaho, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.34140015,-97.73120117&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Brentwood Neighborhood Park, 6710 Arroyo Seco, Austin, TX 78757, USA
    ##   1801 Santa Clara St, Austin, TX 78757, USA
    ##   6800 Yates Ave, Austin, TX 78757, USA
    ##   Brentwood Neighborhood Park Trail, Austin, TX 78757, USA
    ##   Brentwood, Austin, TX, USA
    ##   Austin, TX 78757, USA
    ##   Austin, TX, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-22.92010498,-43.33070374&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Estr. Dr. Azeredo Lopes, 1150 - Freguesia de Jacarepaguá, Rio de Janeiro - RJ, 22743-530, Brazil
    ##   Linha Amarela, 3103 - Freguesia de Jacarepaguá, Rio de Janeiro - RJ, Brazil
    ##   Linha Amarela - Água Santa, Rio de Janeiro - RJ, Brazil
    ##   Rio de Janeiro - State of Rio de Janeiro, Brazil
    ##   Freguesia, Rio de Janeiro - State of Rio de Janeiro, Brazil
    ##   Rio de Janeiro, State of Rio de Janeiro, Brazil
    ##   State of Rio de Janeiro, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.84820557,-84.35820007&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3488 Lakeside Dr NE, Atlanta, GA 30326, USA
    ##   3478 Lakeside Dr NE, Atlanta, GA 30326, USA
    ##   3412 Oak Valley Rd NE, Atlanta, GA 30326, USA
    ##   3399-3455 Oak Valley Rd NE, Atlanta, GA 30326, USA
    ##   Buckhead Heights, Atlanta, GA 30326, USA
    ##   Atlanta, GA 30326, USA
    ##   Atlanta, GA, USA
    ##   Fulton County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=18.51330566,73.84989929&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   734, RB Kumthekar Rd, Perugate, Sadashiv Peth, Pune, Maharashtra 411030, India
    ##   664, RB Kumthekar Rd, Perugate, Sadashiv Peth, Pune, Maharashtra 411030, India
    ##   Unnamed Road, Perugate, Sadashiv Peth, Pune, Maharashtra 411030, India
    ##   Sadashiv Peth, Pune, Maharashtra, India
    ##   Pune, Maharashtra 411030, India
    ##   Pune, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.75100708,-97.8219986&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.61090088,-122.3302994&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Freeway Park, Unnamed Road, Seattle, WA 98101, United States
    ##   1325 9th Ave, Seattle, WA 98101, USA
    ##   800 Convention Pl, Seattle, WA 98101, USA
    ##   1343 Hubbell Pl, Seattle, WA 98101, USA
    ##   1399-1359 Hubbell Pl, Seattle, WA 98101, USA
    ##   First Hill, Seattle, WA, USA
    ##   Seattle, WA 98101, USA
    ##   Downtown Seattle, Seattle, WA, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.13830566,-80.99559784&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   535 Locust St, Port Orange, FL 32127, USA
    ##   541 Locust St, Port Orange, FL 32127, USA
    ##   500 Locust St, Port Orange, FL 32127, USA
    ##   599-501 Locust St, Port Orange, FL 32127, USA
    ##   PT ORANGE, FL 32127, USA
    ##   Port Orange, FL, USA
    ##   Volusia County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.56739807,-117.1757965&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   39767 Ranchwood Dr, Murrieta, CA 92563, USA
    ##   39798 Avenida Miguel Oeste, Murrieta, CA 92563, USA
    ##   Rancho Acacias Park, 39785 Avenida Palizada, Murrieta, CA 92563, USA
    ##   39771 Ranchwood Dr, Murrieta, CA 92563, USA
    ##   Murrieta, CA 92563, USA
    ##   Murrieta, CA, USA
    ##   Riverside County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.62770081,-95.57900238&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4431 S Main St, Stafford, TX 77477, USA
    ##   4307 S Main St, Stafford, TX 77477, USA
    ##   4270 US-90 ALT, Stafford, TX 77477, USA
    ##   US-90 ALT, Stafford, TX 77477, USA
    ##   Stafford, TX 77477, USA
    ##   Fort Bend County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=9.967102051,76.29040527&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.98750305,-84.1167984&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3610 Copper Ridge Rd, Knoxville, TN 37931, USA
    ##   3609 Copper Ridge Rd, Knoxville, TN 37931, USA
    ##   8398-8300 W Emory Rd, Knoxville, TN 37931, USA
    ##   Karns, TN 37931, USA
    ##   Knoxville, TN 37931, USA
    ##   Knox County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.146698,-117.5802994&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10291 Lupine Ct, Rancho Cucamonga, CA 91737, USA
    ##   1029 Lupine Ct, Rancho Cucamonga, CA 91737, USA
    ##   10201 Lupine Ct, Rancho Cucamonga, CA 91737, USA
    ##   10398-10200 Lupine Ct, Rancho Cucamonga, CA 91737, USA
    ##   Alta Loma, CA 91737, USA
    ##   Rancho Cucamonga, CA, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.62950134,-122.3164978&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Volunteer Park, 1247 15th Ave E, Seattle, WA 98112, USA
    ##   Volunteer Park Rd, Seattle, WA 98102, USA
    ##   Capitol Hill, Seattle, WA, USA
    ##   Seattle, WA 98112, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=10.52630615,76.21200562&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7, AR Menon Rd, Naikkanal, Thrissur, Kerala 680020, India
    ##   19, AR Menon Rd, Naikkanal, Thrissur, Kerala 680020, India
    ##   Kodungallur - Shornur Rd, Naikkanal, Thrissur, Kerala 680020, India
    ##   Round West, Thrissur, Kerala, India
    ##   Thrissur, Kerala 680020, India
    ##   Thrissur, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.48190308,-121.4024048&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7604 Countryfield Dr, Sacramento, CA 95828, USA
    ##   8228 Tanya Ln, Sacramento, CA 95828, USA
    ##   8196 Gerber Rd, Sacramento, CA 95828, USA
    ##   Gerber Rd, Sacramento, CA 95828, USA
    ##   Florin, CA, USA
    ##   Sacramento, CA 95828, USA
    ##   Sacramento County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.65879822,-73.84380341&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   158-52 89th St, Jamaica, NY 11414, USA
    ##   158-64 89th St, Howard Beach, NY 11414, USA
    ##   89-99-89-1 159th Ave, Howard Beach, NY 11414, USA
    ##   Howard Beach, Queens, NY, USA
    ##   Howard Beach, NY 11414, USA
    ##   Queens, NY, USA
    ##   Queens County, Queens, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.17230225,-77.18299866&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8700 Snouffer School Rd, Gaithersburg, MD 20879, USA
    ##   19141 Kinglet Pl, Montgomery Village, MD 20879, USA
    ##   8898-8800 Swallow Ct, Montgomery Village, MD 20879, USA
    ##   Montgomery Village, MD, USA
    ##   MONTGOMRY VLG, MD 20879, USA
    ##   9, MD, USA
    ##   Montgomery County, MD, USA
    ##   Maryland, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.63380432,-112.2065964&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   16503 N 69th Ave, Peoria, AZ 85382, USA
    ##   6840 W Judy Lynn Ln, Peoria, AZ 85382, USA
    ##   6883 W Kings Ave, Peoria, AZ 85382, USA
    ##   6860-6874 W Kings Ave, Peoria, AZ 85382, USA
    ##   Peoria, AZ 85382, USA
    ##   Glendale, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-29.76669312,-51.1499939&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Rua Presidente Roosevelt, 966 - Centro, São Leopoldo - RS, 93010-060, Brazil
    ##   Rua Presidente Roosevelt, 980 - Centro, São Leopoldo - RS, 93020-190, Brazil
    ##   Rua Presidente Roosevelt, 977 - Centro, São Leopoldo - RS, 93020-190, Brazil
    ##   Rua Presidente Roosevelt, 1078-998 - Centro, São Leopoldo - RS, 93020-190, Brazil
    ##   Rua Presidente Roosevelt - Centro, São Leopoldo - RS, 93010-060, Brazil
    ##   Centro, São Leopoldo - RS, 93020-190, Brazil
    ##   São Leopoldo - RS, Brazil
    ##   São Leopoldo, RS, Brazil
    ##   State of Rio Grande do Sul, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.18789673,-90.4285965&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   20100 S Buck Creek Rd, Festus, MO 63028, USA
    ##   21533 S Buck Creek Rd, Festus, MO 63028, USA
    ##   21830-21646 S Buck Creek Rd, Festus, MO 63028, USA
    ##   Plattin Township, MO, USA
    ##   Festus, MO 63028, USA
    ##   Jefferson County, MO, USA
    ##   Missouri, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-30.11560059,-51.16529846&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road - Belém Velho, Porto Alegre - RS, Brazil
    ##   Belém Velho, Porto Alegre - RS, Brazil
    ##   Porto Alegre - RS, Brazil
    ##   Porto Alegre, RS, Brazil
    ##   State of Rio Grande do Sul, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.60020447,-74.14689636&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Computer Science, Loop Rd, Staten Island, NY 10314, USA
    ##   Loop Rd, Staten Island, NY 10314, USA
    ##   Staten Island, NY 10314, USA
    ##   Mid Island, Staten Island, NY, USA
    ##   Richmond County, Staten Island, NY, USA
    ##   Staten Island, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.75889587,-97.32800293&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   703 E 1st St, Fort Worth, TX 76102, USA
    ##   704 E Weatherford St, Fort Worth, TX 76102, USA
    ##   167 Alread Ct, Fort Worth, TX 76102, USA
    ##   Sundance Square, Fort Worth, TX 76102, USA
    ##   Fort Worth, TX 76102, USA
    ##   Fort Worth, TX, USA
    ##   Tarrant County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.26379395,-76.65450287&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   121 Clark Rd, Hershey, PA 17033, USA
    ##   46 Highland Rd, Hershey, PA 17033, USA
    ##   149-121 Clark Rd, Hershey, PA 17033, USA
    ##   Hershey, PA, USA
    ##   Hershey, PA 17033, USA
    ##   Derry Township, PA, USA
    ##   Dauphin County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.00320435,-96.54340363&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   400 Willow Way, Wylie, TX 75098, USA
    ##   1202 S Birmingham St, Wylie, TX 75098, USA
    ##   382 Willow Way, Wylie, TX 75098, USA
    ##   609-403 Willow Way, Wylie, TX 75098, USA
    ##   Wylie, TX, USA
    ##   Wylie, TX 75098, USA
    ##   Collin County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=8.179000854,77.43231201&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.6519928,-79.94439697&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1138 Chestnut Ridge Rd, Morgantown, WV 26505, USA
    ##   1065 Suncrest Towne Centre Drive, Morgantown, WV 26505, USA
    ##   1013 County Rte 61, Morgantown, WV 26505, USA
    ##   Suncrest Towne Centre Drive, Morgantown, WV 26505, USA
    ##   Morgantown, WV 26505, USA
    ##   Eastern, WV, USA
    ##   Monongalia County, WV, USA
    ##   West Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.99879456,-74.42610168&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Charlotteburg Rd, Butler, NJ 07405, USA
    ##   98 Butternut Terrace, Kinnelon, NJ 07405, USA
    ##   Kinnelon, NJ 07405, USA
    ##   Butler, NJ 07405, USA
    ##   Morris County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.40280151,-97.86229706&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   605 N 11th St, Enid, OK 73701, USA
    ##   613 N 11th St, Enid, OK 73701, USA
    ##   1001-1099 E Walnut Ave, Enid, OK 73701, USA
    ##   Enid, OK, USA
    ##   Enid, OK 73701, USA
    ##   Garfield County, OK, USA
    ##   Oklahoma, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.76789856,-77.45339966&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8556 Sandstone Way, Manassas Park, VA 20111, USA
    ##   8601 Centreville Rd, Manassas, VA 20111, USA
    ##   8611-8603 Centreville Rd, Manassas, VA 20110, USA
    ##   Manassas Park, VA 20111, USA
    ##   Brentsville, VA, USA
    ##   Prince William County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.78889465,-96.80210114&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   14 Woodall Rodgers Fwy, Dallas, TX 75201, USA
    ##   Klyde Warren Park, 2012 Woodall Rodgers Fwy, Dallas, TX 75201, USA
    ##   Woodall Rodgers Fwy, Dallas, TX 75201, USA
    ##   Dallas, TX 75201, USA
    ##   Dallas, TX, USA
    ##   Dallas County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=9.919006348,78.11950684&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2-b, Kaaval Kooda St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   17, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   23, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   Madurai Main, Madurai, Tamil Nadu, India
    ##   Madurai, Tamil Nadu 625001, India
    ##   Madurai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.16819763,-115.2165985&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5501-5599 Mayflower Ln, Las Vegas, NV 89107, USA
    ##   408 Upland Blvd, Las Vegas, NV 89107, USA
    ##   5508 Mayflower Ln, Las Vegas, NV 89107, USA
    ##   300-398 Zion Dr, Las Vegas, NV 89107, USA
    ##   Las Vegas, NV 89107, USA
    ##   Las Vegas, NV, USA
    ##   Clark County, NV, USA
    ##   Nevada, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.29370117,-79.99019623&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3319 Olivette St NW, Roanoke, VA 24017, USA
    ##   3360 Old Country Club Rd NW, Roanoke, VA 24017, USA
    ##   1084 Old Country Club Rd NW, Roanoke, VA 24017, USA
    ##   1045-1079 Old Country Club Rd NW, Roanoke, VA 24017, USA
    ##   Roanoke, VA 24017, USA
    ##   Roanoke, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.7756958,-112.4730988&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2060 Mohave St, Chino Valley, AZ 86323, USA
    ##   2049 Mohave St, Chino Valley, AZ 86323, USA
    ##   2065 Mohave St, Chino Valley, AZ 86323, USA
    ##   1178-1306 W Rd 3 N, Chino Valley, AZ 86323, USA
    ##   Chino Valley, AZ, USA
    ##   Chino Valley, AZ 86323, USA
    ##   Yavapai County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.92849731,-83.6332016&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   218 Church St, Grand Blanc, MI 48439, USA
    ##   Physicians Park, 218 Reid Rd, Grand Blanc, MI 48439, USA
    ##   SBD Saginaw at Tim Horton's, Grand Blanc, MI 48439, USA
    ##   210 N Church St, Grand Blanc, MI 48439, USA
    ##   Grand Blvd, Grand Blanc, MI 48439, USA
    ##   Grand Blanc, MI 48439, USA
    ##   Genesee County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.28230286,-98.18250275&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2114 Dolly St, Edinburg, TX 78539, USA
    ##   2108 Dolly St, Edinburg, TX 78539, USA
    ##   2102 Dolly St, Edinburg, TX 78539, USA
    ##   2131 Sugar Rd, Edinburg, TX 78539, USA
    ##   2798-2400 Sugar Rd, Edinburg, TX 78539, USA
    ##   Edinburg, TX 78539, USA
    ##   Edinburg, TX, USA
    ##   Hidalgo County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.72569275,-94.62120056&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Garrison, TX 75946, USA
    ##   Nacogdoches County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.13920593,-82.53279877&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3000 SW Shorewood Dr, Dunnellon, FL 34431, USA
    ##   3337 SW Shorewood Dr, Dunnellon, FL 34431, USA
    ##   Dunnellon, FL 34431, USA
    ##   Marion County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.73809814,-75.17469788&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   18498 Seashell Blvd, Lewes, DE 19958, USA
    ##   33118 Seahorse Pl, Lewes, DE 19958, USA
    ##   Lewes, DE 19958, USA
    ##   Sussex County, DE, USA
    ##   Delaware, USA
    ##   Delmarva Peninsula, United States
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   St. Catherine's Park, 1245 1st Avenue, New York, NY 10065, USA
    ##   1245 1st Avenue, New York, NY 10065, USA
    ##   E 67 St & 1 Av, New York, NY 10065, USA
    ##   361 E 67th St, New York, NY 10065, USA
    ##   New York, NY 10065, USA
    ##   Lenox Hill, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.21960449,-83.604599&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   530 Cliffs Dr, Ypsilanti, MI 48198, USA
    ##   5149-5101 Applewood Dr, Ypsilanti, MI 48197, USA
    ##   Ypsilanti Charter Twp, MI, USA
    ##   Ypsilanti, MI 48197, USA
    ##   Washtenaw County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   2-b, Kaaval Kooda St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   17, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   23, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   Madurai Main, Madurai, Tamil Nadu, India
    ##   Madurai, Tamil Nadu 625001, India
    ##   Madurai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=9.947692871,76.2538147&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.92689514,-122.3312988&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   352 S 41st St, Richmond, CA 94804, USA
    ##   Unnamed Road, Richmond, CA 94804, USA
    ##   Park Plaza, Richmond, CA 94804, USA
    ##   Richmond, CA 94804, USA
    ##   Richmond, CA, USA
    ##   Contra Costa County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.96350098,-123.0800018&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2084 Doaks Ferry Rd NW, Salem, OR 97304, USA
    ##   2039 Doaks Ferry Rd NW, Salem, OR 97304, USA
    ##   Doaks Ferry Rd NW, Salem, OR 97304, USA
    ##   2230 Doaks Ferry Rd NW, Salem, OR 97304, USA
    ##   West Salem, Salem, OR 97304, USA
    ##   Salem, OR, USA
    ##   Salem, OR 97304, USA
    ##   Polk County, OR, USA
    ##   Willamette Valley, Oregon, USA
    ##   Oregon, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=1.292892456,103.8547058&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   War Memorial Park, Beach Rd, Singapore 189768
    ##   Beach Rd, Singapore 189768
    ##   Singapore 189768
    ##   Downtown Core, Singapore
    ##   Singapore
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   605 N 11th St, Enid, OK 73701, USA
    ##   613 N 11th St, Enid, OK 73701, USA
    ##   1001-1099 E Walnut Ave, Enid, OK 73701, USA
    ##   Enid, OK, USA
    ##   Enid, OK 73701, USA
    ##   Garfield County, OK, USA
    ##   Oklahoma, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.22000122,-85.69419861&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1708 Blvd Napoleon, Louisville, KY 40205, USA
    ##   Hal Warheim Park, 1832 Overlook Terrace, Louisville, KY 40205, USA
    ##   2424 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   2419 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   1899-1883 Overlook Terrace, Louisville, KY 40205, USA
    ##   Belknap, Louisville, KY 40205, USA
    ##   STRATHMR MNR, KY 40205, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=12.9058075,79.13708496&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   65, Servai Munusamy Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Periyadhanam Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Sankaranpalayam, Vellore, Tamil Nadu 632001, India
    ##   Tamil Nadu 632001, India
    ##   Vellore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.75619507,-122.4866028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1670 28th Ave, San Francisco, CA 94122, USA
    ##   1686 28th Ave, San Francisco, CA 94122, USA
    ##   2201 Lawton St, San Francisco, CA 94122, USA
    ##   1673 28th Ave, San Francisco, CA 94122, USA
    ##   Unnamed Road, San Francisco, CA 94122, USA
    ##   Outer Sunset, San Francisco, CA, USA
    ##   San Francisco, CA 94122, USA
    ##   San Francisco County, CA, USA
    ##   San Francisco, CA, USA
    ##   San Francisco Peninsula, California, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=10.78520203,79.13909912&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Manikund Bus Stop, Gandhiji Rd, Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   73, Gandhiji Rd, Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   137, Gandhiji Rd, Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   Tamil Nadu 613001, India
    ##   Thanjavur, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.80250549,-78.64050293&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   300 W Aycock St, Raleigh, NC 27608, USA
    ##   365 W Aycock St, Raleigh, NC 27608, USA
    ##   232-298 W Aycock St, Raleigh, NC 27608, USA
    ##   Five Points East, Raleigh, NC 27608, USA
    ##   Raleigh, NC 27608, USA
    ##   Raleigh, NC, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.06959534,-79.08180237&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   982 Marineland Pkwy, Allanburg, ON L0S 1A0, Canada
    ##   Marineland Pk & Stanley Av, Niagara Falls, ON L0S 1A0, Canada
    ##   982 Regional Rd 49, Allanburg, ON L0S 1A0, Canada
    ##   Marineland Pkwy, Allanburg, ON L0S 1A0, Canada
    ##   Allanburg, ON L0S 1A0, Canada
    ##   Niagara Falls, ON, Canada
    ##   Regional Municipality of Niagara, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.85209656,-74.9641037&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   65 Matlack Dr, Voorhees Township, NJ 08043, USA
    ##   58 Matlack Dr, Voorhees Township, NJ 08043, USA
    ##   60 Matlack Dr, Voorhees Township, NJ 08043, USA
    ##   62 Matlack Dr, Voorhees Township, NJ 08043, USA
    ##   Kirkwood, NJ 08043, USA
    ##   Voorhees Township, NJ 08043, USA
    ##   Camden County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.76870728,-79.4108963&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   24-44 Princess Ave, North York, ON M2N 6Y6, Canada
    ##   18 Hillcrest Ave, North York, ON M2N 6T5, Canada
    ##   219 Doris Ave, North York, ON M2N 3T5, Canada
    ##   Doris Ave, North York, ON M2N 3T5, Canada
    ##   North York, ON M2N 6T5, Canada
    ##   North York, ON M2N, Canada
    ##   Willowdale, Toronto, ON, Canada
    ##   North York, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   2-b, Kaaval Kooda St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   17, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   23, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   Madurai Main, Madurai, Tamil Nadu, India
    ##   Madurai, Tamil Nadu 625001, India
    ##   Madurai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Township Rd 715, Grande Prairie, AB T8V 7Z8, Canada
    ##   Grande Prairie, AB T8V 7Z8, Canada
    ##   Grande Prairie, AB T8V, Canada
    ##   Grande Prairie, AB, Canada
    ##   Division No. 19, AB, Canada
    ##   Alberta, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.75469971,-73.96140289&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   54 Bond St, New York, NY 10012, USA
    ##   45 Sutton Pl S, New York, NY 10022, USA
    ##   Sutton Place Park South, Sutton Pl S, New York, NY 10022, USA
    ##   63 Sutton Pl S, New York, NY 10022, USA
    ##   E 51st Street Pedestrian Crossing, New York, NY 10022, USA
    ##   New York, NY 10044, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.08650208,-98.28340149&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Reynosa - Nuevo Laredo 220, El Maestro Centro, 88500 Reynosa, Tamps., Mexico
    ##   Aguascalientes 112 esq, Venustiano Carranza, 88500 Reynosa, Tamps., Mexico
    ##   Aguas Calientes 105, El Maestro Centro, 88500 Reynosa, Tamps., Mexico
    ##   Venustiano Carranza 250-220, El Maestro Centro, 88500 Reynosa, Tamps., Mexico
    ##   Ferrocarril Zona Centro, 88500 Reynosa, Tamps., Mexico
    ##   El Maestro Centro, 88500 Reynosa, Tamps., Mexico
    ##   Reynosa, Tamaulipas, Mexico
    ##   Reynosa Municipality, Tamaulipas, Mexico
    ##   Tamaulipas, Mexico
    ##   Mexico
    ## Multiple addresses found, the first will be returned:
    ##   Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   65, Servai Munusamy Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Periyadhanam Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Sankaranpalayam, Vellore, Tamil Nadu 632001, India
    ##   Tamil Nadu 632001, India
    ##   Vellore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   65, Servai Munusamy Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Periyadhanam Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Sankaranpalayam, Vellore, Tamil Nadu 632001, India
    ##   Tamil Nadu 632001, India
    ##   Vellore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.0480957,-77.47280121&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   44163 Paget Terrace, Ashburn, VA 20147, USA
    ##   44171 Paget Terrace, Ashburn, VA 20147, USA
    ##   20521 Ashburn Village Blvd, Ashburn, VA 20147, USA
    ##   Ashburn Village Blvd, Ashburn, VA 20147, USA
    ##   Ashburn, VA, USA
    ##   Broad Run, VA, USA
    ##   Ashburn, VA 20147, USA
    ##   Loudoun County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   2-b, Kaaval Kooda St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   17, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   23, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   Madurai Main, Madurai, Tamil Nadu, India
    ##   Madurai, Tamil Nadu 625001, India
    ##   Madurai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.86810303,-118.1831055&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6228 Myrtle Ave, Long Beach, CA 90805, USA
    ##   801 E Harding St, Long Beach, CA 90805, USA
    ##   899-855 E Harding St, Long Beach, CA 90805, USA
    ##   Jordan, Long Beach, CA 90805, USA
    ##   Long Beach, CA 90805, USA
    ##   Long Beach, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.43249512,-79.86299896&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1501 Ardmore Blvd, Pittsburgh, PA 15221, USA
    ##   538 Sherwood Rd, Pittsburgh, PA 15221, USA
    ##   87 Morrow Rd, Pittsburgh, PA 15221, USA
    ##   Sherwood Rd, Pittsburgh, PA 15221, USA
    ##   Forest Hills, PA, USA
    ##   Pittsburgh, PA 15221, USA
    ##   Allegheny County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.14039612,-80.65139771&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   605 Rockinghorse Rd, Melbourne, FL 32935, USA
    ##   1095 Julia Dr, Melbourne, FL 32935, USA
    ##   1149-1101 Julia Dr, Melbourne, FL 32935, USA
    ##   Carlton Stewart Gardens, Melbourne, FL 32935, USA
    ##   Melbourne, FL 32935, USA
    ##   Melbourne, FL, USA
    ##   Brevard County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.58149719,-81.48500061&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2751 Silver Ridge Dr, Orlando, FL 32818, USA
    ##   2767 Silver Ridge Dr, Orlando, FL 32818, USA
    ##   2762 Silver Ridge Dr, Orlando, FL 32818, USA
    ##   Orlando, FL 32818, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.01109314,-122.875&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1925 Lakewood Dr SE, Olympia, WA 98501, USA
    ##   1903 Lakewood Dr SE, Olympia, WA 98501, USA
    ##   2001 Lakewood Dr SE, Olympia, WA 98501, USA
    ##   1902 Lakewood Dr SE, Olympia, WA 98501, USA
    ##   1821-1899 Lakewood Dr SE, Olympia, WA 98501, USA
    ##   Olympia, WA, USA
    ##   Tumwater, WA 98501, USA
    ##   Thurston County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.37919617,-86.69689941&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5605 Park Side Rd, Hoover, AL 35244, USA
    ##   Oak Mountain Lake Rd, Birmingham, AL 35242, USA
    ##   5603 Oak Mountain Lake Rd, Birmingham, AL 35242, USA
    ##   Pelham, AL, USA
    ##   Birmingham, AL 35242, USA
    ##   Shelby County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.08540344,-111.9682007&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   100200026, Layton, UT 84041, United States
    ##   1777 N Belvedere Way, Layton, UT 84041, USA
    ##   Layton, UT 84041, USA
    ##   Layton, UT, USA
    ##   Davis County, UT, USA
    ##   Utah, USA
    ##   Rocky Mountains
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.63439941,-81.62210083&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Apopka, FL 32703, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=10.8170929,78.69848633&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9/32a, Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   26, Mannarpillai Street, Tharanallur, Tiruchirappalli, Tamil Nadu, India
    ##   9, Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   Tharanallur, Tiruchirappalli, Tamil Nadu, India
    ##   Tiruchirappalli, Tamil Nadu 620002, India
    ##   Tiruchirappalli, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=11.34320068,77.72769165&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   550, Nethaji Rd, Erode Fort, Erode, Tamil Nadu 638001, India
    ##   Manikoondu Bus Stop, Nethaji Rd, Erode Fort, Erode, Tamil Nadu 638001, India
    ##   15, Kongalamman Kovil St, Erode Fort, Erode, Tamil Nadu 638001, India
    ##   Nethaji Rd, Erode Fort, Erode, Tamil Nadu 638001, India
    ##   Erode Fort, Erode, Tamil Nadu 638001, India
    ##   Tamil Nadu 638001, India
    ##   Erode, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.03129578,-118.3124008&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2131 W 27th St, Los Angeles, CA 90018, USA
    ##   2700 S St Andrews Pl, Los Angeles, CA 90018, USA
    ##   2113 W 27th St, Los Angeles, CA 90018, USA
    ##   S St Andrews Pl, Los Angeles, CA 90018, USA
    ##   Jefferson, Culver City, CA, USA
    ##   Los Angeles, CA 90018, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.12939453,-95.42379761&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1126 Rayford Rd, Spring, TX 77386, USA
    ##   1054 Rayford Rd, Spring, TX 77386, USA
    ##   Spring, TX 77386, USA
    ##   Montgomery County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.06820679,-97.39199829&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3909 Sumac Dr, Temple, TX 76502, USA
    ##   3929 Loop Dr, Temple, TX 76502, USA
    ##   3908 Sumac Dr, Temple, TX 76502, USA
    ##   Temple, TX, USA
    ##   Temple, TX 76502, USA
    ##   Bell County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.08210754,-78.4260025&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   400 N Union St, Olean, NY 14760, USA
    ##   Unnamed Road, Olean, NY 14760, USA
    ##   Olean, NY 14760, USA
    ##   Cattaraugus County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.03300476,-73.76519775&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   31 Mamaroneck Ave # 4, White Plains, NY 10601, USA
    ##   1 City Pl, White Plains, NY 10601, USA
    ##   255 Main St, White Plains, NY 10601, USA
    ##   City Pl, White Plains, NY 10601, USA
    ##   White Plains, NY 10601, USA
    ##   White Plains, NY, USA
    ##   Westchester County, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.79119873,-95.41819763&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1000 E T C Jester Blvd, Houston, TX 77008, USA
    ##   979 T C Jester Blvd, Houston, TX 77008, USA
    ##   White Oak Bayou Greenway Trail, Houston, TX 77008, USA
    ##   Lazybrook / Timbergrove, Houston, TX, USA
    ##   Houston, TX 77008, USA
    ##   Houston, TX, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   605 N 11th St, Enid, OK 73701, USA
    ##   613 N 11th St, Enid, OK 73701, USA
    ##   1001-1099 E Walnut Ave, Enid, OK 73701, USA
    ##   Enid, OK, USA
    ##   Enid, OK 73701, USA
    ##   Garfield County, OK, USA
    ##   Oklahoma, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.37199402,-111.7332993&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   801 N 400 E St, Pleasant Grove, UT 84062, USA
    ##   801 N 400 E, Pleasant Grove, UT 84062, USA
    ##   784 N 400 E St, Pleasant Grove, UT 84062, USA
    ##   Pleasant Grove, UT, USA
    ##   Pleasant Grove, UT 84062, USA
    ##   Utah County, UT, USA
    ##   Utah, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.21659851,-117.3908005&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Mojave Fwy, San Bernardino, CA 92407, USA
    ##   San Bernardino, CA, USA
    ##   DEVORE HGHTS, CA 92407, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.84869385,-122.2209015&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   North Oakland Regional Sports Center, 6900 Broadway, Oakland, CA 94611, USA
    ##   6900 Broadway, Oakland, CA 94611, USA
    ##   6413 Swainland Rd, Oakland, CA 94611, USA
    ##   Broadway, Oakland, CA 94611, USA
    ##   Merriewood, Oakland, CA, USA
    ##   Piedmont, CA 94611, USA
    ##   Oakland, CA, USA
    ##   Alameda County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.30389404,-110.8367996&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5277 N Sunset Shadows Pl, Tucson, AZ 85750, USA
    ##   The Old Giuseppe Trail, Tucson, AZ 85750, USA
    ##   5242 N Sunset Shadows Pl, Tucson, AZ 85750, USA
    ##   Quail Canyon, Catalina Foothills, AZ 85750, USA
    ##   Tucson, AZ 85750, USA
    ##   Catalina Foothills, AZ, USA
    ##   Pima County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.66969299,-81.46260071&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   312 Ash St, Fernandina Beach, FL 32034, USA
    ##   310 Ash St, Fernandina Beach, FL 32034, USA
    ##   369 Ash St, Fernandina Beach, FL 32034, USA
    ##   499-401 Ash St, Fernandina Beach, FL 32034, USA
    ##   Fernandina Beach, FL 32034, USA
    ##   Amelia Island, Florida 32034, USA
    ##   FERNANDINA, FL 32034, USA
    ##   Nassau County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.9855957,-93.26550293&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2 Hennepin Ave, Minneapolis, MN 55401, USA
    ##   Unnamed Road, Minneapolis, MN 55401, United States
    ##   W River Pkwy, Minneapolis, MN 55401, USA
    ##   1 1st Ave NE, Minneapolis, MN 55401, USA
    ##   Warehouse District, Minneapolis, MN, USA
    ##   Gateway District, Minneapolis, MN, USA
    ##   Minneapolis, MN 55401, USA
    ##   Minneapolis, MN, USA
    ##   Hennepin County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.87989807,-87.97820282&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   517 Ardmore Ave, Villa Park, IL 60181, USA
    ##   528 S Cornell Ave, Villa Park, IL 60181, USA
    ##   520 Ardmore Ave, Villa Park, IL 60181, USA
    ##   Villa Park, IL, USA
    ##   Oakbrook Terrace, IL 60181, USA
    ##   York Township, IL, USA
    ##   Dupage County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.76530457,-73.95890045&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   St. Catherine's Park, 1245 1st Avenue, New York, NY 10065, USA
    ##   1245 1st Avenue, New York, NY 10065, USA
    ##   E 67 St & 1 Av, New York, NY 10065, USA
    ##   360 E 68th St, New York, NY 10065, USA
    ##   New York, NY 10065, USA
    ##   Lenox Hill, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.88830566,-71.39450073&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   54 Sumner Ave, Central Falls, RI 02863, USA
    ##   70 Sumner Ave, Central Falls, RI 02863, USA
    ##   52 Sumner Ave, Central Falls, RI 02863, USA
    ##   55-87 Fuller Ave, Central Falls, RI 02863, USA
    ##   Central Falls, RI 02863, USA
    ##   Providence County, RI, USA
    ##   Rhode Island, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.01150513,-76.43840027&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10 Spyglass Hill Dr, Bloomsburg, PA 17815, USA
    ##   10 Spyglass Hill Rd, Bloomsburg, PA 17815, USA
    ##   1197 Highland Dr, Bloomsburg, PA 17815, USA
    ##   20 Spyglass Hill Rd, Bloomsburg, PA 17815, USA
    ##   100 Spyglass Hill Rd, Bloomsburg, PA 17815, USA
    ##   Scott, PA, USA
    ##   Bloomsburg, PA 17815, USA
    ##   Columbia County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.03219604,-118.2835999&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Hoover Recreation Center, 1010 W 25th St, Los Angeles, CA 90007, USA
    ##   Hoover / Adams, Los Angeles, CA 90007, USA
    ##   1009 W Adams Blvd, Los Angeles, CA 90007, USA
    ##   1032 W 25th St, Los Angeles, CA 90007, USA
    ##   2563 S Hoover St, Los Angeles, CA 90007, USA
    ##   1112-1100 W Adams Blvd, Los Angeles, CA 90007, USA
    ##   University Park, Los Angeles, CA, USA
    ##   Dockweiler, CA 90007, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.46490479,-90.68289948&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2073 Emily Dr, Dubuque, IA 52003, USA
    ##   1695 Kathy Dr, Dubuque, IA 52003, USA
    ##   2084-2074 Emily Dr, Dubuque, IA 52003, USA
    ##   2140 Jaeger Dr, Dubuque, IA 52003, USA
    ##   Dubuque, IA, USA
    ##   Dubuque, IA 52003, USA
    ##   Dubuque County, IA, USA
    ##   Iowa, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.36669922,-88.09249878&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Idlewild Park, 1013 Idlewild Dr, Round Lake Beach, IL 60073, USA
    ##   1013 Idlewild Dr, Round Lake Beach, IL 60073, USA
    ##   405 Beachview Dr, Round Lake Beach, IL 60073, USA
    ##   925-1003 N Clarendon Dr, Round Lake Beach, IL 60073, USA
    ##   Round Lake Beach, IL, USA
    ##   Round Lake Heights, IL 60073, USA
    ##   Avon Township, IL, USA
    ##   Lake County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.58940125,-122.740097&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6941 N Central St, Portland, OR 97203, USA
    ##   8774 N Burr Ave, Portland, OR 97203, USA
    ##   Unnamed Road, Portland, OR 97203, USA
    ##   St. Johns, Portland, OR, USA
    ##   Portland, OR 97203, USA
    ##   Portland, OR, USA
    ##   Multnomah County, OR, USA
    ##   Oregon, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.65080261,-79.4803009&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   266 Durie St, Toronto, ON M6S 3G3, Canada
    ##   457 Windermere Ave, Toronto, ON M6S 3L5, Canada
    ##   455-537 Windermere Ave, Toronto, ON M6S 3L5, Canada
    ##   Bloor West Village, Toronto, ON, Canada
    ##   Toronto, ON M6S 3G3, Canada
    ##   Toronto, ON M6S, Canada
    ##   Old Toronto, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.66799927,-97.35910034&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1630 W Harry St, Wichita, KS 67213, USA
    ##   1336 S Millwood Ave, Wichita, KS 67213, USA
    ##   1631 Dooley St, Wichita, KS 67213, USA
    ##   1500-1598 Dooley St, Wichita, KS 67213, USA
    ##   McCormick, Wichita, KS 67213, USA
    ##   Wichita, KS 67213, USA
    ##   Wichita, KS, USA
    ##   Sedgwick County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.90750122,-117.7865982&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3007 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   3702 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   S Ridge Trail, Yorba Linda, CA 92886, USA
    ##   Yorba Linda, CA 92886, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.49949646,-86.3640976&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4100 Chapman Rd, Millbrook, AL 36054, USA
    ##   3963 Chapman Rd, Millbrook, AL 36054, USA
    ##   4100-4000 Chapman Rd, Millbrook, AL 36054, USA
    ##   Millbrook, AL 36054, USA
    ##   Elmore County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.58169556,-75.32550049&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2137 Wassergass Rd, Hellertown, PA 18055, USA
    ##   2000 Wirth Rd, Hellertown, PA 18055, USA
    ##   2099-2001 Wirth Rd, Hellertown, PA 18055, USA
    ##   Hellertown, PA 18055, USA
    ##   Lower Saucon Township, PA, USA
    ##   Northampton County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.66130066,-112.0398026&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   19121 N 19th Pl, Phoenix, AZ 85024, USA
    ##   19198 N 19th Pl, Phoenix, AZ 85024, USA
    ##   19117-19199 N 19th Pl, Phoenix, AZ 85024, USA
    ##   Buffalo Ridge Park, 19250 N 16th St, Phoenix, AZ 85024, USA
    ##   Phoenix, AZ 85024, USA
    ##   Paradise Valley Village, Phoenix, AZ, USA
    ##   Phoenix, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.12559509,-93.17359924&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Fort Polk, LA 71459, USA
    ##   Leesville, LA 71459, USA
    ##   11, LA, USA
    ##   Vernon Parish, LA, USA
    ##   Louisiana, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-22.48739624,-42.71150208&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Cachoeiras de Macacu - RJ, 28680-000, Brazil
    ##   Cachoeiras de Macacu - State of Rio de Janeiro, 28680-000, Brazil
    ##   State of Rio de Janeiro, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.80749512,-94.91570282&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   740 Pinewood St, Gardner, KS 66030, USA
    ##   756 Redwood St, Gardner, KS 66030, USA
    ##   701 Pinewood St, Gardner, KS 66030, USA
    ##   782-700 Pinewood St, Gardner, KS 66030, USA
    ##   Gardner, KS, USA
    ##   Gardner, KS 66030, USA
    ##   Johnson County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.98060608,-78.84259796&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Birchwood Park, 3105 Hursey St, Durham, NC 27703, USA
    ##   3105 Hursey St, Durham, NC 27703, USA
    ##   10 Kramer Pl, Durham, NC 27703, USA
    ##   462 Lynn Rd, Durham, NC 27703, USA
    ##   3022-3082 Hursey St, Durham, NC 27703, USA
    ##   Durham, NC 27703, USA
    ##   Oak Grove, NC, USA
    ##   Durham, NC, USA
    ##   Durham County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.77870178,-96.82170105&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Margaret Hunt Hill Bridge, Margaret Hunt Hill Bridge, Dallas, TX 75207, USA
    ##   Trinity Skyline Trail, Dallas, TX 75207, USA
    ##   1001 Continental St Via, Dallas, TX 75212, USA
    ##   Dallas, TX 75207, USA
    ##   Dallas, TX, USA
    ##   Dallas County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.92799377,-77.26490021&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1700 Burlwood Ct, Vienna, VA 22182, USA
    ##   9328 Old Courthouse Rd, Vienna, VA 22182, USA
    ##   7711-1701 Burlwood Ct, Vienna, VA 22182, USA
    ##   Wolf Trap, VA, USA
    ##   Vienna, VA 22182, USA
    ##   Hunter Mill, VA, USA
    ##   Fairfax County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.33039856,-121.7913055&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3157 Norwood Ave, San Jose, CA 95148, USA
    ##   3155 Norwood Ave, San Jose, CA 95148, USA
    ##   3199-3163 Norwood Ave, San Jose, CA 95148, USA
    ##   Centerwood, San Jose, CA 95148, USA
    ##   San Jose, CA 95148, USA
    ##   San Jose, CA, USA
    ##   Santa Clara County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.68769836,-73.92669678&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Citizens for a Better Community Garden, 742 Monroe St, Brooklyn, NY 11221, USA
    ##   742 Monroe St, Brooklyn, NY 11221, USA
    ##   749 Madison St, Brooklyn, NY 11221, USA
    ##   706-770 Madison St, Brooklyn, NY 11221, USA
    ##   Brooklyn, NY 11221, USA
    ##   Bedford-Stuyvesant, Brooklyn, NY, USA
    ##   Brooklyn, NY, USA
    ##   Kings County, Brooklyn, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.04989624,-83.92279816&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3755 Ludo Rd, Knoxville, TN 37918, USA
    ##   Fountain City Ballfields, 3701 Ludo Rd, Knoxville, TN 37918, USA
    ##   3775 Tocar Rd, Knoxville, TN 37918, USA
    ##   3700-3774 Tocar Rd, Knoxville, TN 37918, USA
    ##   Knoxville, TN 37918, USA
    ##   Knoxville, TN, USA
    ##   Knox County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.11680603,-80.08370209&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   305 McConnell Landing, Kernersville, NC 27284, USA
    ##   8911 McConnell Dr, Kernersville, NC 27284, USA
    ##   McConnell Dr, Kernersville, NC 27284, USA
    ##   Kernersville, NC 27284, USA
    ##   Kernersville, NC, USA
    ##   Forsyth County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.90570068,-77.0318985&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1377 Massachusetts Ave NW, Washington, DC 20005, USA
    ##   Massachusetts Ave NW, Washington, DC 20005, USA
    ##   Logan Circle, Washington, DC, USA
    ##   Washington, DC 20005, USA
    ##   Downtown, Washington, DC, USA
    ##   Washington, DC, USA
    ##   District of Columbia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.41389465,-75.68270111&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Jackson Terrace Park, 1300 Jackson St, Scranton, PA 18504, USA
    ##   1300 Jackson St, Scranton, PA 18504, USA
    ##   1316 Jackson St, Scranton, PA 18504, USA
    ##   1307 Jackson St, Scranton, PA 18504, USA
    ##   199-101 S Bromley Ave, Scranton, PA 18504, USA
    ##   Scranton, PA 18504, USA
    ##   Scranton, PA, USA
    ##   Lackawanna County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.11039734,-83.11309814&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6992 Dublin Rd, Dublin, OH 43017, USA
    ##   Emerald Pkwy, Dublin, OH 43016, USA
    ##   6997 OH-745, Dublin, OH 43017, USA
    ##   Dublin, OH 43016, USA
    ##   Dublin, OH, USA
    ##   Franklin County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.57310486,-122.7046051&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1348 Lake Dr, Bremerton, WA 98312, USA
    ##   Cedarwood Dr, Bremerton, WA 98312, USA
    ##   Bremerton, WA, USA
    ##   Bremerton, WA 98312, USA
    ##   Kitsap County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1377 Massachusetts Ave NW, Washington, DC 20005, USA
    ##   Massachusetts Ave NW, Washington, DC 20005, USA
    ##   Logan Circle, Washington, DC, USA
    ##   Washington, DC 20005, USA
    ##   Downtown, Washington, DC, USA
    ##   Washington, DC, USA
    ##   District of Columbia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.42480469,-83.19509888&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   18302 Coyle St, Detroit, MI 48235, USA
    ##   18294 Coyle St, Detroit, MI 48235, USA
    ##   18369 Coyle St, Detroit, MI 48235, USA
    ##   18599-18401 Coyle St, Detroit, MI 48235, USA
    ##   Detroit, MI 48235, USA
    ##   Detroit, MI, USA
    ##   Wayne County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.28070068,-83.78009796&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Maple + Jackson, Ann Arbor, MI 48103, USA
    ##   2500 Jackson Ave, Ann Arbor, MI 48103, USA
    ##   75 S Maple Rd, Ann Arbor, MI 48103, USA
    ##   2392 I-94BL, Ann Arbor, MI 48103, USA
    ##   Unnamed Road, Ann Arbor, MI 48103, USA
    ##   Abbot, Ann Arbor, MI 48103, USA
    ##   Ann Arbor, MI, USA
    ##   Ann Arbor, MI 48103, USA
    ##   Washtenaw County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.98249817,-78.53759766&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   12279 Capital Blvd, Wake Forest, NC 27587, USA
    ##   12400 Wake Union Church Rd, Wake Forest, NC 27587, USA
    ##   12517 US-1, Wake Forest, NC 27587, USA
    ##   US-1, Wake Forest, NC 27587, USA
    ##   Wake Forest, NC 27587, USA
    ##   Wake Forest, NC, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=25.59719849,-80.40480042&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   18405 SW 132nd Ave, Miami, FL 33177, USA
    ##   18400 SW 131st Ave, Miami, FL 33177, USA
    ##   12481 Eureka Dr, Miami, FL 33177, USA
    ##   Eureka Dr, Miami, FL 33177, USA
    ##   Miami, FL 33177, USA
    ##   Miami-Dade County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.47770691,-85.11699677&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   169 Lee Rd 0501, Phenix City, AL 36870, USA
    ##   Lee County Rd 501, Phenix City, AL 36870, USA
    ##   Phenix City, AL 36870, USA
    ##   Lee County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=12.97709656,77.58709717&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1/A, Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka 560001, India
    ##   Unnamed Road, Ambedkar Veedhi, Bengaluru, Karnataka 560001, India
    ##   Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka, India
    ##   Bengaluru, Karnataka 560001, India
    ##   Bengaluru, Karnataka, India
    ##   Bangalore Urban, Karnataka, India
    ##   Karnataka, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   William Steinmetz Park, 1545 S Stimson Ave, Hacienda Heights, CA 91745, USA
    ##   1545 S Stimson Ave, Hacienda Heights, CA 91745, USA
    ##   15906 Three Palms St, Hacienda Heights, CA 91745, USA
    ##   Unnamed Road, Hacienda Heights, CA 91745, USA
    ##   Hacienda Heights, CA, USA
    ##   Hacienda Heights, CA 91745, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47,8&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Nesslisboden, 6113 Romoos, Switzerland
    ##   6113 Romoos, Switzerland
    ##   Romoos, Switzerland
    ##   Entlebuch District, Switzerland
    ##   Lucerne, Switzerland
    ##   Switzerland
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.2230072,-122.5361023&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Homestead Park, 3715 Bridgeport Way W, University Place, WA 98466, USA
    ##   3801 Bridgeport Way W, University Place, WA 98466, USA
    ##   Bridgeport Way W & 37th St W, University Place, WA 98466, USA
    ##   3773 Bridgeport Way W, University Place, WA 98466, USA
    ##   Bridgeport Way W, University Place, WA 98466, USA
    ##   University Place, WA, USA
    ##   Tacoma, WA 98466, USA
    ##   Pierce County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.95970154,-75.19950104&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Saunders Park, 3827 Powelton Ave, Philadelphia, PA 19104, USA
    ##   300-50 Saunders Ave, Philadelphia, PA 19104, USA
    ##   329 N 39th St, Philadelphia, PA 19104, USA
    ##   3914-3900 Powelton Ave, Philadelphia, PA 19104, USA
    ##   West Powelton, Philadelphia, PA, USA
    ##   Philadelphia, PA 19104, USA
    ##   Philadelphia, PA, USA
    ##   Philadelphia County, Philadelphia, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.73829651,-122.4555969&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   125 Dalewood Way, San Francisco, CA 94127, USA
    ##   174 Dalewood Way, San Francisco, CA 94127, USA
    ##   Unnamed Road, San Francisco, CA 94127, USA
    ##   Mount Davidson, San Francisco, CA 94127, USA
    ##   San Francisco, CA 94127, USA
    ##   San Francisco County, CA, USA
    ##   San Francisco, CA, USA
    ##   San Francisco Peninsula, California, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.51539612,-97.66889954&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1110 Brushy Creek Dr, Round Rock, TX 78664, USA
    ##   1001 North Georgetown Street, Round Rock, TX 78664, USA
    ##   1107 Brushy Creek Dr, Round Rock, TX 78664, USA
    ##   301-313 Pecan Ln, Round Rock, TX 78664, USA
    ##   Brushy Slope Addition, Round Rock, TX 78664, USA
    ##   Round Rock, TX 78664, USA
    ##   Round Rock, TX, USA
    ##   Williamson County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   2837 S Maple Grove Rd, Boise, ID 83709, USA
    ##   Molenaar Park, 2815 S Maple Grove Rd, Boise, ID 83709, USA
    ##   2815 S Maple Grove Rd, Boise, ID 83709, USA
    ##   2768 S Maple Grove Rd, Boise, ID 83709, USA
    ##   2485-2743 S Maple Grove Rd, Boise, ID 83709, USA
    ##   Southwest Ada County Alliance, Boise, ID 83709, USA
    ##   Boise, ID 83709, USA
    ##   Boise, ID, USA
    ##   Ada County, ID, USA
    ##   Idaho, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.4223938,-88.18450165&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   137 S 7th Ave, West Bend, WI 53095, USA
    ##   139 S 7th Ave, West Bend, WI 53095, USA
    ##   146 S 6th Ave, West Bend, WI 53095, USA
    ##   664 Walnut St, West Bend, WI 53095, USA
    ##   799-701 Walnut St, West Bend, WI 53095, USA
    ##   West Bend, WI, USA
    ##   West Bend, WI 53095, USA
    ##   Washington County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.55490112,-122.2707977&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   899 Balboa Ln, Foster City, CA 94404, USA
    ##   800-898 Balboa Ln, Foster City, CA 94404, USA
    ##   Foster City, CA 94404, USA
    ##   Foster City, CA, USA
    ##   San Francisco Peninsula, California, USA
    ##   San Mateo County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=27.87190247,-82.63710022&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10960 1st Ln N, St. Petersburg, FL 33716, USA
    ##   390 112th Ave N, St. Petersburg, FL 33716, USA
    ##   10985 1st Ln N, St. Petersburg, FL 33716, USA
    ##   Unnamed Road, St. Petersburg, FL 33716, USA
    ##   St. Petersburg, FL 33716, USA
    ##   St. Petersburg, FL, USA
    ##   Pinellas County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.37750244,-79.96130371&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3528 Willett Rd, Pittsburgh, PA 15227, USA
    ##   3536 Willett Rd, Pittsburgh, PA 15227, USA
    ##   Brentwood, PA 15227, USA
    ##   Baldwin, PA, USA
    ##   Allegheny County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.88989258,-85.6147995&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2013 43rd St SE, Grand Rapids, MI 49508, USA
    ##   3836 Kentridge Dr SE, Grand Rapids, MI 49508, USA
    ##   2050 Eastcastle Dr SE, Grand Rapids, MI 49508, USA
    ##   2034-2048 Eastcastle Dr SE, Grand Rapids, MI 49508, USA
    ##   Millbrook, Grand Rapids, MI 49508, USA
    ##   Kentwood, MI 49508, USA
    ##   Grand Rapids, MI, USA
    ##   Kent County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.52209473,-122.8585052&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   17742 NW Pioneer Rd, Beaverton, OR 97006, USA
    ##   17664 NW Shady Fir Loop, Beaverton, OR 97006, USA
    ##   Triple Creek, Beaverton, OR 97006, USA
    ##   Hillsboro, OR 97006, USA
    ##   Beaverton, OR, USA
    ##   Washington County, OR, USA
    ##   Willamette Valley, Oregon, USA
    ##   Oregon, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.59719849,-79.69309998&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Mississauga, ON L5V 0B6, Canada
    ##   Mississauga, ON L5V, Canada
    ##   East Credit, Mississauga, ON, Canada
    ##   Mississauga, ON, Canada
    ##   Regional Municipality of Peel, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.05180359,-94.40460205&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3715 S Phelps Rd, Independence, MO 64055, USA
    ##   3800 S Crane St, Independence, MO 64055, USA
    ##   3805 S Phelps Rd, Independence, MO 64055, USA
    ##   3719 S Phelps Rd, Independence, MO 64055, USA
    ##   14511-14899 East 37th St S, Independence, MO 64055, USA
    ##   Independence, MO 64055, USA
    ##   Independence, MO, USA
    ##   Blue Township, MO, USA
    ##   Jackson County, MO, USA
    ##   Missouri, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Freeway Park, Unnamed Road, Seattle, WA 98101, United States
    ##   1325 9th Ave, Seattle, WA 98101, USA
    ##   800 Convention Pl, Seattle, WA 98101, USA
    ##   1343 Hubbell Pl, Seattle, WA 98101, USA
    ##   1399-1359 Hubbell Pl, Seattle, WA 98101, USA
    ##   First Hill, Seattle, WA, USA
    ##   Seattle, WA 98101, USA
    ##   Downtown Seattle, Seattle, WA, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.79449463,-105.0983963&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5367 Field Cir, Arvada, CO 80002, USA
    ##   9070 Ridge Rd, Arvada, CO 80002, USA
    ##   9030 Gyda Dr, Arvada, CO 80002, USA
    ##   9074 Ridge Rd, Arvada, CO 80002, USA
    ##   8929-9015 Gyda Dr, Arvada, CO 80002, USA
    ##   Arvada Plaza Area, Arvada, CO, USA
    ##   Arvada, CO 80002, USA
    ##   Arvada, CO, USA
    ##   Jefferson County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.73640442,-73.86949921&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   56 92nd St, Queens, NY 11373, USA
    ##   92-02 56th Ave, Flushing, NY 11373, USA
    ##   92 St/56 Av, Queens, NY 11373, USA
    ##   92-11 56th Ave, Elmhurst, NY 11373, USA
    ##   55-0-55-98 92nd St, Elmhurst, NY 11373, USA
    ##   Queens, NY 11373, USA
    ##   Elmhurst, Queens, NY, USA
    ##   Queens, NY, USA
    ##   Queens County, Queens, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.87309265,-73.87259674&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3184 Webster Ave, The Bronx, NY 10467, USA
    ##   Bronx River Pkwy, The Bronx, NY 10467, USA
    ##   The Bronx, NY 10467, USA
    ##   The Bronx, NY, USA
    ##   Bronx County, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=46.81469727,-92.19979858&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4949 Trails End Dr, Hermantown, MN 55811, USA
    ##   4936 Trails End Dr, Hermantown, MN 55811, USA
    ##   4877-4903 Trails End Dr, Hermantown, MN 55811, USA
    ##   Hermantown, MN, USA
    ##   Duluth, MN 55811, USA
    ##   St Louis County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.20010376,-118.4456024&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7125 Lennox Ave, Van Nuys, CA 91405, USA
    ##   7136 Lennox Ave, Van Nuys, CA 91405, USA
    ##   7119 Lennox Ave, Van Nuys, CA 91405, USA
    ##   7199-7145 Lennox Ave, Van Nuys, CA 91405, USA
    ##   Valley Glen, CA 91405, USA
    ##   Van Nuys, Los Angeles, CA, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.65960693,-111.9195023&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5003 Meadow View Dr, Taylorsville, UT 84123, USA
    ##   Jordan River Parkway Equestrian Trail, Taylorsville, UT 84123, USA
    ##   5022 Meadow View Dr, Taylorsville, UT 84123, USA
    ##   Salt Lake City, UT 84123, USA
    ##   Taylorsville, UT, USA
    ##   Salt Lake Valley, Utah, USA
    ##   Salt Lake County, UT, USA
    ##   Utah, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=19.97940063,-102.280098&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   General Manuel Ávila Camacho Oriente 448, Jardines de Catedral, 59670 Zamora de Hidalgo, Mich., Mexico
    ##   22 de Octubre Sur 542, Jardines de Catedral, 59670 Zamora de Hidalgo, Mich., Mexico
    ##   5 de Febrero Sur 553-521, Jardines de Catedral, 59670 Zamora de Hidalgo, Mich., Mexico
    ##   Jardines de Catedral, Zamora de Hidalgo, Mich., Mexico
    ##   Jardines de Catedral, 59670 Zamora de Hidalgo, Mich., Mexico
    ##   Zamora, Michoacán, Mexico
    ##   Zamora, Mich., Mexico
    ##   Michoacán, Mexico
    ##   Mexico
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.24090576,-111.7791977&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Citrus Vista Park, 4511 S Mustang Dr, Chandler, AZ 85249, USA
    ##   4511 S Mustang Dr, Chandler, AZ 85249, USA
    ##   3646 E Tonto Pl, Chandler, AZ 85249, USA
    ##   E Tonto Pl, Chandler, AZ 85249, USA
    ##   Chandler, AZ 85249, USA
    ##   Chandler, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.99479675,-87.10369873&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1239 S 300 W, Rensselaer, IN 47978, USA
    ##   1556 S County Rd 300 W, Rensselaer, IN 47978, USA
    ##   Unnamed Road, Collegeville, IN 47978, USA
    ##   Barkley Township, IN, USA
    ##   Rensselaer, IN 47978, USA
    ##   Jasper County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.43800354,-111.7117996&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5544 E Brown Rd, Mesa, AZ 85205, USA
    ##   N Pad, Mesa, AZ 85205, USA
    ##   1460 N Alta Mesa Dr, Mesa, AZ 85205, USA
    ##   Alta Mesa Community Association, Mesa, AZ, USA
    ##   Mesa, AZ 85205, USA
    ##   Mesa, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.87750244,-84.50170135&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3199 Highland Dr SE, Smyrna, GA 30080, USA
    ##   Highland Drive Park, 3209 Highland Dr SE, Smyrna, GA 30080, USA
    ##   3209 Highland Dr SE, Smyrna, GA 30080, USA
    ##   3099 Jonquil Dr, Smyrna, GA 30080, USA
    ##   Smyrna, GA 30080, USA
    ##   Smyrna, GA, USA
    ##   Cobb County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.56910706,-75.16300201&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1341 Centerton Rd, Pittsgrove Township, NJ 08318, USA
    ##   1148-1314 Centerton Rd, Pittsgrove Township, NJ 08318, USA
    ##   Pittsgrove Township, NJ 08318, USA
    ##   Salem County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.81230164,-86.14209747&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   14615 James St, Holland, MI 49424, USA
    ##   14574 James St, Holland, MI 49424, USA
    ##   2612-2624 Lilac Ave, Holland, MI 49424, USA
    ##   Park Township, MI, USA
    ##   Holland, MI 49424, USA
    ##   Ottawa County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.94400024,-94.2881012&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   25301 NE Colbern Rd, Lee's Summit, MO 64086, USA
    ##   25304 County Hwy 8-S, Lee's Summit, MO 64086, USA
    ##   9405 S Howard Rd, Lee's Summit, MO 64064, USA
    ##   25762-25334 County Hwy 8-S, Lee's Summit, MO 64086, USA
    ##   Lee's Summit, MO 64086, USA
    ##   Prairie Township, MO, USA
    ##   Jackson County, MO, USA
    ##   Missouri, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.98469543,-80.44760132&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   109 E Wilson St, Wingate, NC 28174, USA
    ##   116 W Wilson St, Wingate, NC 28174, USA
    ##   107 State Rd 1002, Wingate, NC 28174, USA
    ##   220 N Camden Rd, Wingate, NC 28174, USA
    ##   Unnamed Road, Wingate, NC 28174, USA
    ##   Wingate, NC 28174, USA
    ##   Monroe, NC, USA
    ##   Union County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.93310547,-74.01950073&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   650 Plympton St, New Milford, NJ 07646, USA
    ##   345 Monmouth Ave, New Milford, NJ 07646, USA
    ##   655 Plympton St, New Milford, NJ 07646, USA
    ##   369-363 Monmouth Ave, New Milford, NJ 07646, USA
    ##   New Milford, NJ 07646, USA
    ##   Bergen County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Manikund Bus Stop, Gandhiji Rd, Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   73, Gandhiji Rd, Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   137, Gandhiji Rd, Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   Attar Mohalla, Thanjavur, Tamil Nadu 613001, India
    ##   Tamil Nadu 613001, India
    ##   Thanjavur, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=20,77&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Maharashtra 431703, India
    ##   Hingoli, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.91200256,75.85380554&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   451, Naya Mohalla, Ludhiana, Punjab 141008, India
    ##   Unnamed Road, Naya Mohalla, Ludhiana, Punjab 141008, India
    ##   Naya Mohalla, Ludhiana, Punjab 141008, India
    ##   Punjab 141008, India
    ##   Ludhiana, Punjab, India
    ##   Punjab, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.30360413,-81.5911026&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2200 Sand Hill Rd, Kissimmee, FL 34747, USA
    ##   1416 N Old Lake Wilson Rd, Kissimmee, FL 34747, USA
    ##   Four Corners, FL, USA
    ##   Celebration, FL 34747, USA
    ##   Osceola County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.84820557,-73.78630066&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2 Ivy Ct, Clifton Park, NY 12065, USA
    ##   Ivy Ct, Clifton Park, NY 12065, USA
    ##   Clifton Park, NY 12065, USA
    ##   Clifton Park, NY, USA
    ##   Saratoga County, NY, USA
    ##   Adirondack Mountains
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.47399902,-80.55400085&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   270 Columbia St W, Waterloo, ON N2L, Canada
    ##   University of Waterloo Environmental Reserve, Trans Canada Trail, Waterloo, ON N2L 0A1, Canada
    ##   Columbia St W, Waterloo, ON N2L, Canada
    ##   Waterloo, ON N2L, Canada
    ##   Waterloo, ON, Canada
    ##   Waterloo Regional Municipality, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=12.12399292,78.15478516&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chinnathai Colony, Indhira Nagar, Dharmapuri, Tamil Nadu 636701, India
    ##   Indhira Nagar, Dharmapuri, Tamil Nadu 636701, India
    ##   Chinnathai Colony, Indhira Nagar, Dharmapuri, Tamil Nadu 636701, India
    ##   Dharmapuri, Tamil Nadu, India
    ##   Tamil Nadu 636701, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.60139465,77.19891357&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Ashoka Police Ln, Teen Murti Marg Area, New Delhi, Delhi 110011, India
    ##   Teen Murti Marg Area, New Delhi, Delhi 110011, India
    ##   New Delhi, Delhi 110011, India
    ##   New Delhi, Delhi, India
    ##   Delhi, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.03489685,-82.57479858&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5232 Williamsburg, North Street, MI 48049, USA
    ##   5897 Shoefelt Rd, North Street, MI 48049, USA
    ##   Clyde Township, MI 48049, USA
    ##   North Street, MI 48049, USA
    ##   St Clair County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.61999512,-73.83429718&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   98 Adams Pl, Delmar, NY 12054, USA
    ##   5 Hawthorne Ave, Delmar, NY 12054, USA
    ##   3 Hawthorne Ave, Delmar, NY 12054, USA
    ##   155-165 Adams St, Delmar, NY 12054, USA
    ##   Delmar, NY, USA
    ##   Delmar, NY 12054, USA
    ##   Bethlehem, NY, USA
    ##   Albany County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.30220032,-82.62640381&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   11348 Lakeview Dr, New Port Richey, FL 34654, USA
    ##   11336 Lakeview Dr, New Port Richey, FL 34654, USA
    ##   11355 Lakeview Dr, New Port Richey, FL 34654, USA
    ##   The Reserve At Golden Acres, FL 34654, USA
    ##   NEW PRT RCHY, FL 34654, USA
    ##   Pasco County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.89729309,-95.64630127&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   15715 Pinyon Creek Dr, Houston, TX 77095, USA
    ##   15718 Pinyon Creek Dr, Houston, TX 77095, USA
    ##   15800-15814 Sweetwater Creek Dr, Houston, TX 77095, USA
    ##   Houston, TX 77095, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.03340149,-89.45120239&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   De Volis Park, 4300 De Volis Pkwy, Madison, WI 53711, USA
    ##   4300 De Volis Pkwy, Madison, WI 53711, USA
    ##   4334 De Volis Pkwy, Madison, WI 53711, USA
    ##   4331 De Volis Pkwy, Madison, WI 53711, USA
    ##   Dunn's Marsh, Madison, WI 53711, USA
    ##   Madison, WI 53711, USA
    ##   Madison, WI, USA
    ##   Dane County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.78089905,-73.95020294&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2 Bond St, New York, NY 10012, USA
    ##   303 E 90th St, New York, NY 10128, USA
    ##   Ruppert Park, 1741 2nd Ave, New York, NY 10128, USA
    ##   301 E 90th St, New York, NY 10128, USA
    ##   1736 2nd Ave, New York, NY 10128, USA
    ##   New York, NY 10128, USA
    ##   Yorkville, New York, NY, USA
    ##   Upper East Side, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.54660034,-82.52130127&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8522 Highpoint Blvd, Brooksville, FL 34613, USA
    ##   High Point, FL 34613, USA
    ##   Spring Hill, FL 34613, USA
    ##   Hernando County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.34860229,-75.76110077&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   525 New St, Duryea, PA 18642, USA
    ##   302 McCullen St, Duryea, PA 18642, USA
    ##   531 New St, Duryea, PA 18642, USA
    ##   300 McCullen St, Duryea, PA 18642, USA
    ##   399-301 McCullen St, Duryea, PA 18642, USA
    ##   Pittston, PA 18642, USA
    ##   Duryea, PA, USA
    ##   Luzerne County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.97990417,-76.62290192&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   96 Eyer Rd, Danville, PA 17821, USA
    ##   PA-54, Danville, PA 17821, USA
    ##   78 Hill St, Danville, PA 17821, USA
    ##   Mahoning Township, PA 17821, USA
    ##   Danville, PA 17821, USA
    ##   Montour County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.10699463,-117.594101&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9688 Foothill Blvd, Rancho Cucamonga, CA 91730, USA
    ##   9684 Foothill Blvd, Rancho Cucamonga, CA 91730, USA
    ##   Foothill @ Archibald Wb Fs, Rancho Cucamonga, CA 91730, USA
    ##   9672 Foothill Blvd, Rancho Cucamonga, CA 91730, USA
    ##   Foothill Blvd, Rancho Cucamonga, CA 91730, USA
    ##   Rancho Cucamonga, CA 91730, USA
    ##   Rancho Cucamonga, CA, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.29870605,-82.69020081&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9730 Shamokin Ln, Port Richey, FL 34668, USA
    ##   9726 Shamokin Ln, Port Richey, FL 34668, USA
    ##   9723 Shamokin Ln, Port Richey, FL 34668, USA
    ##   Embassy Hills, Jasmine Estates, FL 34668, USA
    ##   Jasmine Estates, FL, USA
    ##   Port Richey, FL 34668, USA
    ##   Pasco County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.00309753,-121.9171982&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Ripple Rouge Rd, Pittsburg, CA 94565, USA
    ##   2299 John Henry Johnson Pkwy, Pittsburg, CA 94565, USA
    ##   Pittsburg, CA, USA
    ##   Pittsburg, CA 94565, USA
    ##   Contra Costa County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.83700562,-88.90570068&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2261 Barrett Ln, Humboldt, TN 38343, USA
    ##   1829 US-45W, Humboldt, TN 38343, USA
    ##   US-45W, Humboldt, TN 38343, USA
    ##   Humboldt, TN 38343, USA
    ##   Gibson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.31610107,-106.7991028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1417 Stewart Ln, Las Cruces, NM 88005, USA
    ##   1413 Stewart Ln, Las Cruces, NM 88005, USA
    ##   1482 Stewart Ln, Las Cruces, NM 88005, USA
    ##   1000-1198 Eight St, Las Cruces, NM 88005, USA
    ##   Las Cruces, NM, USA
    ##   Las Cruces, NM 88005, USA
    ##   Doña Ana County, NM, USA
    ##   New Mexico, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=54.97349548,-1.567306519&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Welbeck Road-Flodden Street, Newcastle upon Tyne NE6 2NU, UK
    ##   101 Welbeck Rd, Newcastle upon Tyne NE6 2HU, UK
    ##   100 Welbeck Rd, Newcastle upon Tyne NE6, UK
    ##   Welbeck Rd, Newcastle upon Tyne NE6 2NU, UK
    ##   Newcastle upon Tyne NE6, UK
    ##   Newcastle upon Tyne, UK
    ##   Newcastle upon Tyne District, Newcastle upon Tyne, UK
    ##   Tyne and Wear, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=53.33380127,-6.248794556&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Wilton Park House, Wilton Pl, Dublin 2, Ireland
    ##   7 Wilton Pl, Dublin, Ireland
    ##   6 Wilton Pl, Dublin, Ireland
    ##   Wilton Pl, Dublin, Ireland
    ##   Dublin City, Co. Dublin, Ireland
    ##   Dublin, Ireland
    ##   Co. Dublin, Ireland
    ##   Ireland
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.26660156,-118.7642975&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Arroyo Simi Greenway, Simi Valley, CA 93065, USA
    ##   Simi Valley, CA 93065, USA
    ##   Simi Valley, CA, USA
    ##   Ventura County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.90449524,-73.80729675&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   267 Irving Pl, Pelham, NY 10803, USA
    ##   267 Cliff Ave, Pelham, NY 10803, USA
    ##   192 Irving Pl, Pelham, NY 10803, USA
    ##   298-276 Cliff Ave, Pelham, NY 10803, USA
    ##   Village of Pelham, NY, USA
    ##   Pelham, NY, USA
    ##   Pelham, NY 10803, USA
    ##   Westchester County, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.28840637,-95.99720001&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3146 N 54th St, Omaha, NE 68104, USA
    ##   3301 N 54th St, Omaha, NE 68104, USA
    ##   3275 N 54th St, Omaha, NE 68104, USA
    ##   5499-5401 Bedford Ave, Omaha, NE 68104, USA
    ##   Gallagher Park, 2936 N 52nd St, Omaha, NE 68104, USA
    ##   Benson, Omaha, NE, USA
    ##   Omaha, NE 68104, USA
    ##   Omaha, NE, USA
    ##   Douglas County, NE, USA
    ##   Nebraska, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.01759338,-80.99250031&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1350 Turners Rock Rd, Savannah, GA 31410, USA
    ##   135 Johnny Mercer Blvd, Wilmington Island, GA 31410, USA
    ##   Johnny Mercer Blvd, Savannah, GA 31410, USA
    ##   Whitemarsh Island, GA, USA
    ##   Savannah, GA 31410, USA
    ##   Chatham County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.3394928,-118.6983032&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5421 WA-21, Odessa, WA 99159, USA
    ##   Odessa, WA 99159, USA
    ##   Lincoln County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.34320068,-85.84400177&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   204 Timberlake Dr, Enterprise, AL 36330, USA
    ##   205 Timberlake Dr, Enterprise, AL 36330, USA
    ##   1850-1910 Dauphin St Ext, Enterprise, AL 36330, USA
    ##   Enterprise, AL 36330, USA
    ##   Coffee County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.71380615,-89.96579742&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Maryville YMCA, Maryville, IL 62062, USA
    ##   1 Maryville Town Center Dr, Collinsville, IL 62234, USA
    ##   1 Maryville Town Center Dr, Maryville, IL 62062, USA
    ##   25-17 Maryville Town Center Dr, Maryville, IL 62062, USA
    ##   Maryville, IL, USA
    ##   Maryville, IL 62062, USA
    ##   Collinsville Township, IL, USA
    ##   Madison County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.70610046,-83.70439911&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5059 N McCord Rd, Sylvania, OH 43560, USA
    ##   13 Bent Creek Crossing, Sylvania, OH 43560, USA
    ##   12 Bent Creek Crossing, Sylvania, OH 43560, USA
    ##   Bent Creek Crossing, Sylvania, OH 43560, USA
    ##   Sylvania, OH, USA
    ##   Sylvania, OH 43560, USA
    ##   Sylvania Township, OH, USA
    ##   Lucas County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.3874054,-112.0998001&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6428 S 19th Ave, Phoenix, AZ 85041, USA
    ##   19th Av & Alta Vista Rd, Phoenix, AZ 85041, USA
    ##   6501 S 19th Ave, Phoenix, AZ 85041, USA
    ##   1838-1840 W Lydia Ln, Phoenix, AZ 85041, USA
    ##   Phoenix, AZ 85041, USA
    ##   South Mountain Village, Phoenix, AZ, USA
    ##   Phoenix, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.78059387,-79.35030365&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2850 Don Mills Rd W, North York, ON M2J, Canada
    ##   2961 Don Mills Rd W, North York, ON M2J, Canada
    ##   2800 Don Mills Rd E, North York, ON M2J, Canada
    ##   Don Valley Village, Toronto, ON, Canada
    ##   North York, ON M2J, Canada
    ##   North York, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.71569824,-74&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Columbus Park, Mulberry Street &, Baxter St, New York, NY 10013, United States
    ##   95 Bayard St, New York, NY 10013, USA
    ##   78 Baxter St, New York, NY 10013, USA
    ##   35 Baxter St, New York, NY 10013, USA
    ##   New York, NY 10013, USA
    ##   Lower Manhattan, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.66229248,-96.3348999&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2386 W Briargate Dr, Bryan, TX 77802, USA
    ##   2800 Cherry Creek Cir, Bryan, TX 77802, USA
    ##   Bryan, TX 77802, USA
    ##   Bryan, TX, USA
    ##   Brazos County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.55999756,68.77389526&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Abdulahad Kakharov Street, Dushanbe, Tajikistan
    ##   Dushanbe, Tajikistan
    ##   Districts of Republican Subordination, Tajikistan
    ##   Tajikistan
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   9/32a, Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   26, Mannarpillai Street, Tharanallur, Tiruchirappalli, Tamil Nadu, India
    ##   9, Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   Tharanallur, Tiruchirappalli, Tamil Nadu, India
    ##   Tiruchirappalli, Tamil Nadu 620002, India
    ##   Tiruchirappalli, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=23.75180054,90.42541504&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Taltola Market Rd, Dhaka 1219, Bangladesh
    ##   Ward-24, Dhaka, Bangladesh
    ##   Taltola, Dhaka, Bangladesh
    ##   Dcc (Khilgaon), Dhaka, Bangladesh
    ##   Khilgaon, Dhaka, Bangladesh
    ##   Dhaka, Bangladesh
    ##   Dhaka District, Bangladesh
    ##   Dhaka Division, Bangladesh
    ##   Bangladesh
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=10.50480652,-66.92079926&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Plaza El Parnaso, Caracas,, Distrito Capital, Venezuela
    ##   1030 La Planicie, Caracas 1012, Distrito Capital, Venezuela
    ##   Calle La Amargura, Caracas 1020, Distrito Capital, Venezuela
    ##   San Juan, Caracas, Distrito Capital, Venezuela
    ##   Caracas 1020, Capital District, Venezuela
    ##   Libertador, Capital District, Venezuela
    ##   Capital District, Venezuela
    ##   Caracas, Capital District, Venezuela
    ##   Venezuela
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=18.98779297,72.83639526&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   1708 Blvd Napoleon, Louisville, KY 40205, USA
    ##   Hal Warheim Park, 1832 Overlook Terrace, Louisville, KY 40205, USA
    ##   2424 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   2419 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   1899-1883 Overlook Terrace, Louisville, KY 40205, USA
    ##   Belknap, Louisville, KY 40205, USA
    ##   STRATHMR MNR, KY 40205, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.84049988,-117.9525986&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2045 Crescent Ave, Anaheim, CA 92801, USA
    ##   1900 W Crescent Ave, Anaheim, CA 92801, USA
    ##   1982 Crescent Ave, Anaheim, CA 92801, USA
    ##   I-5, Anaheim, CA 92801, USA
    ##   Northwest Anaheim, Anaheim, CA, USA
    ##   Anaheim, CA 92801, USA
    ##   Anaheim, CA, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.69400024,-73.8219986&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   124-19 95th Ave, Jamaica, NY 11419, USA
    ##   12419 95th Ave, South Richmond Hill, NY 11419, USA
    ##   125-19 95th Ave, South Richmond Hill, NY 11419, USA
    ##   124-0-124-98 95th Ave, South Richmond Hill, NY 11419, USA
    ##   South Richmond Hill, Queens, NY, USA
    ##   Jamaica, NY 11419, USA
    ##   Queens, NY, USA
    ##   Queens County, Queens, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   9/32a, Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   26, Mannarpillai Street, Tharanallur, Tiruchirappalli, Tamil Nadu, India
    ##   9, Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   Mannarpillai St, Tharanallur, Tiruchirappalli, Tamil Nadu 620008, India
    ##   Tharanallur, Tiruchirappalli, Tamil Nadu, India
    ##   Tiruchirappalli, Tamil Nadu 620002, India
    ##   Tiruchirappalli, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.92059326,-75.18260193&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2509 S 21st St, Philadelphia, PA 19145, USA
    ##   Stephen Girard Park, 2101 W Shunk St, Philadelphia, PA 19145, USA
    ##   2526 S 21st St, Philadelphia, PA 19145, USA
    ##   2500-2506 S 21st St, Philadelphia, PA 19145, USA
    ##   Girard Estates, Philadelphia, PA 19145, USA
    ##   Philadelphia, PA 19145, USA
    ##   Philadelphia, PA, USA
    ##   Philadelphia County, Philadelphia, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.03900146,-81.73809814&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   553 Park Meadows Ct, Wadsworth, OH 44281, USA
    ##   546 Park Meadows Ct, Wadsworth, OH 44281, USA
    ##   Park Meadows Ct, Wadsworth, OH 44281, USA
    ##   Wadsworth, OH 44281, USA
    ##   Medina County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.02589417,-80.95469666&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5319 Lakeshore Dr, Columbia, SC 29206, USA
    ##   5388 Lakeshore Dr, Columbia, SC 29206, USA
    ##   Unnamed Road, Columbia, SC 29206, USA
    ##   Forest Acres, SC, USA
    ##   Columbia, SC 29206, USA
    ##   Richland County, SC, USA
    ##   South Carolina, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   313, N H 209, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Unnamed Road, Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Anupperpalayam, Ram Nagar, Coimbatore, Tamil Nadu 641009, India
    ##   Coimbatore, Tamil Nadu 641009, India
    ##   Ram Nagar, Coimbatore, Tamil Nadu, India
    ##   Coimbatore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.72619629,-83.15660095&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4935 Mill Creek Dr, Rochester, MI 48306, USA
    ##   4959 Orion Rd, Oakland Charter Township, MI 48306, USA
    ##   Mill Creek Dr, Oakland Charter Township, MI 48306, USA
    ##   Rochester, MI 48306, USA
    ##   Oakland Charter Township, MI, USA
    ##   Oakland County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   WPRWA-94, Santo Gopalan Rd, Chullickal, Kochi, Kerala 682002, India
    ##   MK Raghavan Rd, Chullickal, Kochi, Kerala 682005, India
    ##   Chullickal, Kochi, Kerala, India
    ##   Kochi, Kerala 682002, India
    ##   Kochi, Kerala, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.78860474,-74.16339874&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   315 Belleville Ave, Belleville, NJ 07109, USA
    ##   321 Belleville Ave, Belleville, NJ 07109, USA
    ##   339-327 Belleville Ave, Belleville, NJ 07109, USA
    ##   Belleville, NJ 07109, USA
    ##   Belleville, NJ, USA
    ##   Essex County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.90049744,-122.2472&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.37289429,-121.8560028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   694 Webster Dr, San Jose, CA 95133, USA
    ##   696 Webster Dr, San Jose, CA 95133, USA
    ##   Pacheco, San Jose, CA 95133, USA
    ##   San Jose, CA 95133, USA
    ##   San Jose, CA, USA
    ##   Santa Clara County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   1500 Rose Ln, Raleigh, NC 27610, USA
    ##   Dacian Road Park, 566 Dacian Rd, Raleigh, NC 27610, USA
    ##   570 Rose Ln, Raleigh, NC 27610, USA
    ##   Walnut Creek Trail, Raleigh, NC 27610, USA
    ##   570 Dacian Rd, Raleigh, NC 27610, USA
    ##   Southeast Raleigh, Raleigh, NC, USA
    ##   Raleigh, NC, USA
    ##   Raleigh, NC 27610, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.46069336,-83.45819855&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Orchard Hills West Park, Malott Dr, Novi, MI 48375, USA
    ##   40757 Village Wood Rd, Novi, MI 48375, USA
    ##   41644 Chattman St, Novi, MI 48375, USA
    ##   23197 Ampton St, Novi, MI 48375, USA
    ##   Malott Dr, Novi, MI 48375, USA
    ##   Novi, MI 48375, USA
    ##   Novi, MI, USA
    ##   Oakland County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-2.909194946,-41.77470398&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   R. Josias de Morães Corrêa, 440 - Nova Parnaíba, Parnaíba - PI, 64218-530, Brazil
    ##   R. Josias de Morães Corrêa, 676 - Nova Parnaíba, Parnaíba - PI, 64218-530, Brazil
    ##   R. Josias de Morães Corrêa, 580 - Bebedouro, Parnaíba - PI, 64218-530, Brazil
    ##   Av. Cap. Claro - Centro, Parnaíba - PI, 64200-500, Brazil
    ##   Av. Cap. Claro - Nova Parnaíba, Parnaíba - PI, 64218-610, Brazil
    ##   Nova Parnaíba, Parnaíba - PI, Brazil
    ##   Parnaíba - State of Piauí, Brazil
    ##   Parnaíba, State of Piauí, Brazil
    ##   State of Piauí, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.55039978,-81.1832962&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   606 Waterland Ct, Orlando, FL 32828, USA
    ##   Alafaya, FL 32828, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.28990173,-82.22290039&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   68 Elmwood Pl, Oberlin, OH 44074, USA
    ##   155 Elm St, Oberlin, OH 44074, USA
    ##   137 Elm St, Oberlin, OH 44074, USA
    ##   55 Elmwood Pl, Oberlin, OH 44074, USA
    ##   Oberlin, OH 44074, USA
    ##   Elyria, OH 44074, USA
    ##   Lorain County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.48390198,22.08920288&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Marshal Tito 204, Negotina, North Macedonia
    ##   R1103 204, Negotino, North Macedonia
    ##   Marshal Tito, Negotino, North Macedonia
    ##   Negotino, North Macedonia
    ##   Municipality of Negotino, North Macedonia
    ##   North Macedonia
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   10 Aldermanbury, London EC2V 7RF, UK
    ##   1 Love Ln, London EC2V, UK
    ##   Aldermanbury, London EC2V, UK
    ##   Love Ln, London EC2V 7JN, UK
    ##   London EC2V, UK
    ##   City of London, UK
    ##   City of London, London, UK
    ##   London, UK
    ##   Greater London, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.16169739,74.18829346&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   G.T. Rd, Gujranwala, Punjab, Pakistan
    ##   Old Town, Gujranwala, Punjab, Pakistan
    ##   Gujranwala, Punjab, Pakistan
    ##   Punjab, Pakistan
    ##   Pakistan
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.70069885,-75.74189758&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   William M. Redd, Junior Park, 500 Paper Mill Rd, Newark, DE 19711, USA
    ##   305 Walker Way, Newark, DE 19711, USA
    ##   Redd Park Trail, Newark, DE 19711, USA
    ##   399 Walker Way, Newark, DE 19711, USA
    ##   Newark, DE, USA
    ##   Newark, DE 19711, USA
    ##   New Castle County, DE, USA
    ##   Delaware, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=20.62910461,-103.411499&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Sierra de Pihuamo 1693, Las Águilas, 45080 Zapopan, Jal., Mexico
    ##   Sierra de Pihuamo 1685, Las Águilas, 45080 Zapopan, Jal., Mexico
    ##   Sierra de Pihuamo 1694, Las Águilas, 45080 Zapopan, Jal., Mexico
    ##   Las Águilas, 45080 Zapopan, Jal., Mexico
    ##   Colinas de Las Águilas, 45080 Jal., Mexico
    ##   Zapopan, Jalisco, Mexico
    ##   Jalisco, Mexico
    ##   Mexico
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.01409912,-118.3983002&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Braddock Dr/Le Bourget Ave, Culver City, CA 90232, USA
    ##   4182 Le Bourget Ave, Culver City, CA 90232, USA
    ##   Carlson Park, 4231 Motor Ave, Culver City, CA 90232, USA
    ##   4233 Motor Ave, Culver City, CA 90232, USA
    ##   10433 Braddock Dr, Culver City, CA 90232, USA
    ##   Unnamed Road, Culver City, CA 90232, USA
    ##   Carlson Park, Culver City, CA, USA
    ##   Culver City, CA 90232, USA
    ##   Culver City, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.45530701,-98.56770325&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   520 Fordham, San Antonio, TX 78228, USA
    ##   460 Fordham, San Antonio, TX 78228, USA
    ##   NW 36th St, San Antonio, TX 78228, USA
    ##   San Antonio, TX 78228, USA
    ##   Inner West Side, San Antonio, TX, USA
    ##   San Antonio, TX, USA
    ##   Bexar County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.71470642,-79.95259857&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1531 Harborsun Dr, Charleston, SC 29412, USA
    ##   James Island, Charleston, SC 29412, USA
    ##   Charleston, SC 29412, USA
    ##   Charleston, SC, USA
    ##   Charleston County, SC, USA
    ##   South Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.07910156,-82.52449799&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   14212 Banbury Way, Tampa, FL 33624, USA
    ##   Carrollwood Village Phase II, Greater Carrollwood, FL, USA
    ##   Tampa, FL 33624, USA
    ##   Greater Carrollwood, FL, USA
    ##   Hillsborough County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=53.58299255,9.981292725&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Hegestraße 5, 20251 Hamburg, Germany
    ##   Hoheluft, Hamburg, Germany
    ##   20251 Hamburg, Germany
    ##   Hamburg-Nord, Hamburg, Germany
    ##   Hamburg, Germany
    ##   Germany
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.09640503,-117.8582001&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1577 Cypress St, Covina, CA 91724, USA
    ##   1605 Cypress St, Covina, CA 91724, USA
    ##   1573 Cypress St, Covina, CA 91724, USA
    ##   Cypress St, Covina, CA 91724, USA
    ##   Covina, CA 91724, USA
    ##   Charter Oak, Covina, CA, USA
    ##   Covina, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.91329956,-80.35870361&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   360 Mc Duffie St, Sumter, SC 29150, USA
    ##   330 Mc Duffie St, Sumter, SC 29150, USA
    ##   Cemetery Rd, Sumter, SC 29150, USA
    ##   Sumter, SC, USA
    ##   Oswego, SC 29150, USA
    ##   Sumter County, SC, USA
    ##   South Carolina, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.18919373,-111.5315018&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3154 E Skyline Dr, San Tan Valley, AZ 85140, USA
    ##   San Tan Valley, AZ, USA
    ##   Queen Creek, AZ 85140, USA
    ##   Pinal County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Wilton Park House, Wilton Pl, Dublin 2, Ireland
    ##   7 Wilton Pl, Dublin, Ireland
    ##   6 Wilton Pl, Dublin, Ireland
    ##   Wilton Pl, Dublin, Ireland
    ##   Dublin City, Co. Dublin, Ireland
    ##   Dublin, Ireland
    ##   Co. Dublin, Ireland
    ##   Ireland
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.11669922,-80.12860107&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1310 Brickell Dr, Fort Lauderdale, FL 33301, USA
    ##   1500 Brickell Dr, Fort Lauderdale, FL 33301, USA
    ##   1464 Brickell Dr, Fort Lauderdale, FL 33301, USA
    ##   400-498 Tarpon Dr, Fort Lauderdale, FL 33301, USA
    ##   Colee Hammock, Fort Lauderdale, FL 33301, USA
    ##   Fort Lauderdale, FL 33301, USA
    ##   Fort Lauderdale, FL, USA
    ##   Broward County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=14.62109375,-90.52690125&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Building 31, 30 Calle 31, Guatemala
    ##   2 Avenida A, Guatemala
    ##   Zone 3, Guatemala City, Guatemala
    ##   Guatemala City, Guatemala
    ##   Guatemala Department, Guatemala
    ##   Guatemala
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.96980286,-86.50610352&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   203 N Lowry St, Smyrna, TN 37167, USA
    ##   417 S Lowry St, Smyrna, TN 37167, USA
    ##   468 US-41, Smyrna, TN 37167, USA
    ##   US-41, Smyrna, TN 37167, USA
    ##   Smyrna, TN, USA
    ##   Smyrna, TN 37167, USA
    ##   Rutherford County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.1835022,-94.17620087&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   328 S 40th St, Springdale, AR 72762, USA
    ##   328 N 40th St, Springdale, AR 72762, USA
    ##   Springdale, AR, USA
    ##   Springdale Township, AR, USA
    ##   Springdale, AR 72762, USA
    ##   Washington County, AR, USA
    ##   Arkansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.47279358,-77.59059906&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1301 Hybla Rd, Richmond, VA 23236, USA
    ##   10400 Dakins Dr, Richmond, VA 23236, USA
    ##   1300 Hybla Rd, Richmond, VA 23236, USA
    ##   1399-1301 Hybla Rd, Richmond, VA 23236, USA
    ##   North Chesterfield, VA 23236, USA
    ##   Clover Hill, VA, USA
    ##   Chesterfield County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-23.63000488,-46.63220215&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   R. Abraão Miguel do Carmo, 548 - Vila Monte Alegre, São Paulo - SP, 04306-090, Brazil
    ##   Av. Afonso D'Escragnolle Taunay, 3972 - Vila Monte Alegre, São Paulo - SP, Brazil
    ##   R. Abraão Miguel do Carmo, São Paulo - SP, Brazil
    ##   Vila Monte Alegre, São Paulo - SP, Brazil
    ##   São Paulo - State of São Paulo, Brazil
    ##   São Paulo, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.21479797,-98.23100281&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1218 Kendlewood Ave, McAllen, TX 78501, USA
    ##   1201 Maple Ave, McAllen, TX 78501, USA
    ##   1220 N 12th St, McAllen, TX 78501, USA
    ##   1299-1201 N 12th St, McAllen, TX 78501, USA
    ##   McAllen, TX 78501, USA
    ##   McAllen, TX, USA
    ##   Hidalgo County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.61430359,-87.32510376&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1956 Well Line Rd, Cantonment, FL 32533, USA
    ##   102 Morris Ave, Cantonment, FL 32533, USA
    ##   Morris Ave, Cantonment, FL 32533, USA
    ##   Cantonment, FL 32533, USA
    ##   Escambia County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.4776001,-75.7059021&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   26 Rue Clermont, Gatineau, QC J8T 5H8, Canada
    ##   32 Rue Clermont, Gatineau, QC J8T 5H8, Canada
    ##   Pierre-lafontaine/vassal, Gatineau, QC J8T 5H1, Canada
    ##   436 Rue Vassal, Gatineau, QC J8T, Canada
    ##   Gatineau, QC J8T 5H8, Canada
    ##   District des Promenades, Gatineau, QC J8T, Canada
    ##   Gatineau, QC J8T, Canada
    ##   Gatineau, QC, Canada
    ##   Communauté-Urbaine-de-l'Outaouais, QC, Canada
    ##   Quebec, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.47070313,9.188903809&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Via Brera, 28, 20121 Milano MI, Italy
    ##   Via Brera, 14, 20121 Milano MI, Italy
    ##   Piazzetta di Brera, 2, 20121 Milano MI, Italy
    ##   Piazzetta di Brera, 1, 20121 Milano MI, Italy
    ##   Brera, 20121 Milano MI, Italy
    ##   20121 Milan, Metropolitan City of Milan, Italy
    ##   Milan, Metropolitan City of Milan, Italy
    ##   Metropolitan City of Milan, Italy
    ##   Lombardy, Italy
    ##   Italy
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.96879578,-86.44029999&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   925 N Washington Ave, Ludington, MI 49431, USA
    ##   908 N Washington Ave, Ludington, MI 49431, USA
    ##   990 N Emily St, Ludington, MI 49431, USA
    ##   N Emily St, Ludington, MI 49431, USA
    ##   Ludington, MI 49431, USA
    ##   Mason County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.02839661,-117.2872009&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2279 S Wild Canyon Dr, Colton, CA 92324, USA
    ##   2273 S Cres Cir, Colton, CA 92324, USA
    ##   Colton, CA, USA
    ##   Colton, CA 92324, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.26339722,-85.67299652&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Brownsboro @ Lightfoot, Louisville, KY 40207, USA
    ##   405 Lightfoot Rd, Louisville, KY 40207, USA
    ##   3420 US-42, Louisville, KY 40207, USA
    ##   3338-3398 US-42, Louisville, KY 40207, USA
    ##   Crescent Hill, Louisville, KY, USA
    ##   BRWNSBORO VLG, KY 40207, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.14639282,-81.51069641&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Portage Trail Extension W, Cuyahoga Falls, OH 44223, USA
    ##   Cuyahoga Falls, OH 44223, USA
    ##   Cuyahoga Falls, OH, USA
    ##   Summit County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.06750488,-118.3520966&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5900 Metropolitan Plaza, Los Angeles, CA 90036, USA
    ##   399 S Fuller Ave, Los Angeles, CA 90036, USA
    ##   412-400 S Burnside Ave, Los Angeles, CA 90036, USA
    ##   La Brea, Los Angeles, CA, USA
    ##   Los Angeles, CA 90036, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.95500183,-85.36530304&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   502 Alden Nash Ave SE, Lowell, MI 49331, USA
    ##   Vergennes Township, MI, USA
    ##   Lowell, MI 49331, USA
    ##   Kent County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.74099731,9.13079834&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Via Fiammenghini, 18, 22063 Cantù CO, Italy
    ##   Via Fiammenghini, 25, 22063 Cantù CO, Italy
    ##   22063 Cantù, Province of Como, Italy
    ##   Province of Como, Italy
    ##   Lombardy, Italy
    ##   Italy
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.39390564,-81.42160034&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3312 Whisper Lakes Blvd, Orlando, FL 32837, USA
    ##   11822 Ottawa Ave, Orlando, FL 32837, USA
    ##   2631 Taber Ct, Orlando, FL 32837, USA
    ##   2620-2636 Taber Ct, Orlando, FL 32837, USA
    ##   Orlando, FL 32837, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.28500366,-78.86540222&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   950 Scalp Ave, Johnstown, PA 15904, USA
    ##   890 Scalp Ave, Johnstown, PA 15904, USA
    ##   928 Scalp Ave, Johnstown, PA 15904, USA
    ##   Richland, PA, USA
    ##   Johnstown, PA 15904, USA
    ##   Cambria County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.03529358,-94.46360016&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4720 Pittman Rd, Kansas City, MO 64133, USA
    ##   9848 E 48 St, Kansas City, MO 64133, USA
    ##   9801-9849 E 48 St, Kansas City, MO 64133, USA
    ##   Stayton Meadows, Kansas City, MO 64133, USA
    ##   Raytown, MO 64133, USA
    ##   Blue Township, MO, USA
    ##   Kansas City, MO, USA
    ##   Jackson County, MO, USA
    ##   Missouri, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.71170044,-71.16629791&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Plainsman Park, Chestnut St &, White St, Lawrence, MA 01841, United States
    ##   46 White St, Lawrence, MA 01841, USA
    ##   353 Elm St, Lawrence, MA 01841, USA
    ##   Elm Towers, Lawrence, Lawrence, MA 01841, USA
    ##   85 White St, Lawrence, MA 01841, USA
    ##   115-199 White St, Lawrence, MA 01841, USA
    ##   Lawrence, MA 01841, USA
    ##   Lawrence, MA, USA
    ##   Essex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.07679749,-73.48529816&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7 Parsons Walk, Darien, CT 06820, USA
    ##   6 Parsons Walk, Darien, CT 06820, USA
    ##   45-31 Old Parish Rd, Darien, CT 06820, USA
    ##   Darien, CT 06820, USA
    ##   Darien, CT, USA
    ##   Fairfield County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.11099243,-84.30249786&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   815 Cooper Sandy Cove, Alpharetta, GA 30004, USA
    ##   110 Cooper Sandy Pointe, Alpharetta, GA 30004, USA
    ##   100 Cooper Sandy Pointe, Milton, GA 30004, USA
    ##   101-119 Cooper Sandy Pointe, Milton, GA 30004, USA
    ##   Alpharetta, GA 30009, USA
    ##   Milton, GA, USA
    ##   Fulton County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1708 Blvd Napoleon, Louisville, KY 40205, USA
    ##   Hal Warheim Park, 1832 Overlook Terrace, Louisville, KY 40205, USA
    ##   2424 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   2419 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   1899-1883 Overlook Terrace, Louisville, KY 40205, USA
    ##   Belknap, Louisville, KY 40205, USA
    ##   STRATHMR MNR, KY 40205, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.04840088,-92.49479675&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Northgate Park, 2107 24th St NW, Rochester, MN 55901, USA
    ##   2107 24th St NW, Rochester, MN 55901, USA
    ##   2438 21st Ave NW, Rochester, MN 55901, USA
    ##   2436 21st Ave NW, Rochester, MN 55901, USA
    ##   2599-2501 23rd Ave NW, Rochester, MN 55901, USA
    ##   Rochester, MN 55901, USA
    ##   Rochester, MN, USA
    ##   Olmsted County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.79469299,-82.9285965&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1157 Carver Ridge Rd, Portsmouth, OH 45662, USA
    ##   509 Township Hwy 324, Portsmouth, OH 45662, USA
    ##   Clay Township, OH, USA
    ##   Sciotoville, OH 45662, USA
    ##   Scioto County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   2-b, Kaaval Kooda St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   17, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   23, S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   S Chitrai St, Valaiyal Kadai, Madurai Main, Madurai, Tamil Nadu 625001, India
    ##   Madurai Main, Madurai, Tamil Nadu, India
    ##   Madurai, Tamil Nadu 625001, India
    ##   Madurai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.27830505,-111.7198029&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1183-1299 Event Center Dr, Orem, UT 84058, USA
    ##   1251 Event Center Dr, Orem, UT 84058, USA
    ##   College Dr, Orem, UT 84058, USA
    ##   Sunset Heights, Orem, UT, USA
    ##   Orem, UT, USA
    ##   Orem, UT 84058, USA
    ##   Utah County, UT, USA
    ##   Utah, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   65, Servai Munusamy Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Periyadhanam Subbarayan Street, Velapadi, Vellore, Tamil Nadu 632001, India
    ##   Sankaranpalayam, Vellore, Tamil Nadu 632001, India
    ##   Tamil Nadu 632001, India
    ##   Vellore, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.7256012,-87.8588028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   710 S Emmertsen Rd, Mt Pleasant, WI 53406, USA
    ##   523 Green Valley Dr, Mt Pleasant, WI 53406, USA
    ##   470-522 Green Valley Dr, Mt Pleasant, WI 53406, USA
    ##   Racine, WI 53406, USA
    ##   Mt Pleasant, WI, USA
    ##   Racine County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=27.84469604,-97.59549713&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   11504 Rippling Creek Cir, Corpus Christi, TX 78410, USA
    ##   4204 Wandering Creek Dr, Corpus Christi, TX 78410, USA
    ##   11507 Rippling Creek Cir, Corpus Christi, TX 78410, USA
    ##   Wandering Creek Dr, Corpus Christi, TX 78410, USA
    ##   Calallen, Corpus Christi, TX, USA
    ##   CORP CHRISTI, TX 78410, USA
    ##   Corpus Christi, TX, USA
    ##   Nueces County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.45530701,-86.62850189&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   947 Ashley Ln, Fort Walton Beach, FL 32547, USA
    ##   946 Ashley Ln, Fort Walton Beach, FL 32547, USA
    ##   945-947 Ashley Ln, Fort Walton Beach, FL 32547, USA
    ##   Fort Walton Beach, FL, USA
    ##   Fort Walton Beach, FL 32547, USA
    ##   Okaloosa County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.95899963,-95.45140076&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   11903 Swords Creek Rd, Houston, TX 77067, USA
    ##   1731 Hugh Rd, Houston, TX 77067, USA
    ##   11901 Swords Creek Rd, Houston, TX 77067, USA
    ##   T C Jester Blvd, Houston, TX 77067, USA
    ##   Houston, TX 77067, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.84869385,-117.2767029&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   939 Coast Blvd, La Jolla, CA 92037, USA
    ##   103 Coast Blvd, La Jolla, CA 92037, USA
    ##   940 Coast Blvd, La Jolla, CA 92037, USA
    ##   1022-1000 Coast Blvd, La Jolla, CA 92037, USA
    ##   La Jolla, CA 92037, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=27.79200745,-80.48069763&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   115 Harbor Point Dr, Sebastian, FL 32958, USA
    ##   345 S Wimbrow Dr, Sebastian, FL 32958, USA
    ##   199 Harbor Point Dr, Sebastian, FL 32958, USA
    ##   100-198 Harbor Point Dr, Sebastian, FL 32958, USA
    ##   Sebastian, FL, USA
    ##   Sebastian, FL 32958, USA
    ##   Indian River County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.08999634,-75.03630066&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1600 Fulmer St, Philadelphia, PA 19115, USA
    ##   1699-1601 Fulmer St, Philadelphia, PA 19115, USA
    ##   Bustleton, Philadelphia, PA, USA
    ##   Philadelphia, PA 19115, USA
    ##   Philadelphia, PA, USA
    ##   Philadelphia County, Philadelphia, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.99490356,-88.03639984&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   99 W Cleveland Ave, West Allis, WI 53227, USA
    ##   Cleveland & S99 #8448, West Allis, WI 53227, USA
    ##   2723 S 99th St, West Allis, WI 53227, USA
    ##   9750-9898 W Cleveland Ave, West Allis, WI 53227, USA
    ##   Milwaukee, WI 53227, USA
    ##   West Allis, WI, USA
    ##   Milwaukee County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.98139954,-88.05120087&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   21W771 Thorndale Ave, Medinah, IL 60157, USA
    ##   7N225 Medinah Rd, Medinah, IL 60157, USA
    ##   22W132 Thorndale Ave, Medinah, IL 60157, United States
    ##   21 Thorndale Ave, Medinah, IL 60157, USA
    ##   7 Medinah Rd, Medinah, IL 60157, USA
    ##   Medinah, IL 60157, USA
    ##   Medinah, IL, USA
    ##   Bloomingdale Township, IL, USA
    ##   Dupage County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=54.04789734,-2.797698975&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Dalton Square Lancaster, Dalton Square, Lancaster LA1 1PL, UK
    ##   5 Dalton Square, Lancaster LA1, UK
    ##   Dalton Square, Lancaster LA1, UK
    ##   Dalton Square, Lancaster LA1 1PL, UK
    ##   Lancaster, UK
    ##   Lancaster LA1, UK
    ##   Lancaster District, UK
    ##   Lancashire, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.4730072,-73.49780273&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8 Twin Rocks Dr, New Fairfield, CT 06812, USA
    ##   6 Old Bridge Rd E, New Fairfield, CT 06812, USA
    ##   Pembroke Rd, New Fairfield, CT 06812, USA
    ##   New Fairfield, CT 06812, USA
    ##   New Fairfield, CT, USA
    ##   Fairfield County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Wilton Park House, Wilton Pl, Dublin 2, Ireland
    ##   7 Wilton Pl, Dublin, Ireland
    ##   6 Wilton Pl, Dublin, Ireland
    ##   Wilton Pl, Dublin, Ireland
    ##   Dublin City, Co. Dublin, Ireland
    ##   Dublin, Ireland
    ##   Co. Dublin, Ireland
    ##   Ireland
    ## Multiple addresses found, the first will be returned:
    ##   R. Abraão Miguel do Carmo, 548 - Vila Monte Alegre, São Paulo - SP, 04306-090, Brazil
    ##   Av. Afonso D'Escragnolle Taunay, 3972 - Vila Monte Alegre, São Paulo - SP, Brazil
    ##   R. Abraão Miguel do Carmo, São Paulo - SP, Brazil
    ##   Vila Monte Alegre, São Paulo - SP, Brazil
    ##   São Paulo - State of São Paulo, Brazil
    ##   São Paulo, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   305 McConnell Landing, Kernersville, NC 27284, USA
    ##   8911 McConnell Dr, Kernersville, NC 27284, USA
    ##   McConnell Dr, Kernersville, NC 27284, USA
    ##   Kernersville, NC 27284, USA
    ##   Kernersville, NC, USA
    ##   Forsyth County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.01519775,28.93159485&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Sehremini, Börekçi Veli Sk. No:16, 34104 Fatih/Istanbul, Turkey
    ##   Sehremini, Börekçi Veli Sk. No:3, 34104 Fatih/Istanbul, Turkey
    ##   Sehremini, 34104 Fatih/Istanbul, Turkey
    ##   Fatih/Istanbul, Turkey
    ##   Istanbul, Turkey
    ##   Turkey
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.90390015,-84.56900024&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   726 E Shotwell St, Bainbridge, GA 39819, USA
    ##   718 Georgia 1 Business, Bainbridge, GA 39819, USA
    ##   799-721 GA-38 BUS, Bainbridge, GA 39819, USA
    ##   Bainbridge, GA, USA
    ##   Bainbridge, GA 39819, USA
    ##   Decatur County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.55589294,-121.7391052&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1026 J St, Davis, CA 95616, USA
    ##   1024 J St, Davis, CA 95616, USA
    ##   1043 J St, Davis, CA 95616, USA
    ##   Davis, CA, USA
    ##   Davis, CA 95616, USA
    ##   Yolo County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.74499512,-75.31990051&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   129 N Convent Ave, Nazareth, PA 18064, USA
    ##   2 N Convent Ave, Nazareth, PA 18064, USA
    ##   43-1 N Convent Ave, Nazareth, PA 18064, USA
    ##   Nazareth, PA 18064, USA
    ##   Northampton County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.55569458,-72.66320038&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   383 Washington St, Middletown, CT 06457, USA
    ##   Unnamed Road, Middletown, CT 06457, USA
    ##   Middletown, CT, USA
    ##   Middletown, CT 06457, USA
    ##   Middlesex County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.82229614,-83.28289795&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   121 Frederick Dr, Oxford, MI 48371, USA
    ##   101 Davis Lake Dr, Oxford, MI 48371, USA
    ##   129 Frederick Dr, Oxford, MI 48371, USA
    ##   Eugene Dr, Oxford, MI 48371, USA
    ##   Oxford Charter Township, MI, USA
    ##   Oxford, MI 48371, USA
    ##   Oakland County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=54.54499817,-6.256103516&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8 Drumart Cres, Ballinderry Lower, Lisburn BT28 2LS, UK
    ##   6 Drumart Cres, Lisburn BT28 2BF, UK
    ##   2 B12, Lisburn BT28 2BF, UK
    ##   Millvale, Ballinderry Lower, Lisburn BT28 2FA, UK
    ##   Lisburn BT28, UK
    ##   Lisburn, UK
    ##   Lisburn and Castlereagh, UK
    ##   Northern Ireland, UK
    ##   Ireland
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=55.8802948,-4.305496216&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   57 Hyndland Rd, Glasgow G12 9UX, UK
    ##   63 Hyndland Rd, Glasgow G12 9UX, UK
    ##   Hughenden Rd, Glasgow G12, UK
    ##   Hyndland Rd, Glasgow G12 9UT, UK
    ##   Glasgow G12, UK
    ##   Glasgow City, Glasgow, UK
    ##   Glasgow, UK
    ##   Scotland, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.83079529,-118.1125031&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3948 Gondar Ave, Long Beach, CA 90808, USA
    ##   3938 Gondar Ave, Long Beach, CA 90808, USA
    ##   6126 Parkcrest St, Long Beach, CA 90808, USA
    ##   6199-6151 Parkcrest St, Long Beach, CA 90808, USA
    ##   Long Beach, CA 90808, USA
    ##   Long Beach, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.40100098,-80.8687973&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   13117 McCoy Rd, Huntersville, NC 28078, USA
    ##   9105 Cedar River Rd, Huntersville, NC 28078, USA
    ##   9534 Kincey Ave, Huntersville, NC 28078, USA
    ##   13106 McCoy Rd, Huntersville, NC 28078, USA
    ##   McCoy Rd, Huntersville, NC 28078, USA
    ##   Huntersville, NC, USA
    ##   Huntersville, NC 28078, USA
    ##   Mecklenburg County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.94270325,-93.28710175&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3303 Garfield Ave, Minneapolis, MN 55408, USA
    ##   3250 Garfield Ave, Minneapolis, MN 55408, USA
    ##   3317 Garfield Ave, Minneapolis, MN 55408, USA
    ##   3312 Garfield Ave, Minneapolis, MN 55408, USA
    ##   500-598 W 33rd St, Minneapolis, MN 55408, USA
    ##   Minneapolis, MN 55408, USA
    ##   Powderhorn, Minneapolis, MN, USA
    ##   Minneapolis, MN, USA
    ##   Hennepin County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.6618042,-91.54090118&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   170 English Philosophy Building, Iowa City, IA 52242-1486, Iowa City, IA 52242, United States
    ##   251 W Iowa Ave, Iowa City, IA 52245, USA
    ##   Iowa River rc Trail, Iowa City, IA 52246, USA
    ##   Iowa City, IA 52246, USA
    ##   Iowa City, IA, USA
    ##   Hills, IA, USA
    ##   Johnson County, IA, USA
    ##   Iowa, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.63189697,-79.37159729&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.85479736,-74.02839661&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   85 Waterside Dr, Little Ferry, NJ 07643, USA
    ##   19 Cedar St, Ridgefield Park, NJ 07660, USA
    ##   30 Spruce Ave, Ridgefield Park, NJ 07660, USA
    ##   Industrial Ave, Ridgefield Park, NJ 07660, USA
    ##   1 Hobart St, Ridgefield Park, NJ 07660, USA
    ##   Ridgefield Park, NJ, USA
    ##   Little Ferry, NJ 07643, USA
    ##   Bergen County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.1546936,-84.5911026&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   McFarlan Woods, Mt. Airy Forest, Mc Farlan Ridge Rd, Cincinnati, OH 45211, USA
    ##   Westwood Northern Blvd & McFarland Woods, Cincinnati, OH 45211, USA
    ##   2884 Westwood Northern Blvd, Cincinnati, OH 45211, USA
    ##   2603 Vienna Woods Dr, Cincinnati, OH 45211, USA
    ##   Mc Farlan Ridge Rd, Cincinnati, OH 45211, USA
    ##   Westwood, Cincinnati, OH, USA
    ##   Cincinnati, OH 45211, USA
    ##   Cincinnati, OH, USA
    ##   Hamilton County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.5052948,-84.52929688&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   385 Eli Ln, Oneida, TN 37841, USA
    ##   180 Eli Ln, Oneida, TN 37841, USA
    ##   356 Burchfield Ave, Oneida, TN 37841, USA
    ##   229 Eli Ln, Oneida, TN 37841, USA
    ##   358-368 Eli Ln, Oneida, TN 37841, USA
    ##   Oneida, TN 37841, USA
    ##   Scott County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.03219604,-79.8588028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3812 Frazier Rd, Greensboro, NC 27407, USA
    ##   3804 Frazier Rd, Greensboro, NC 27407, USA
    ##   3802 Frazier Rd, Greensboro, NC 27407, USA
    ##   3931 Wintergarden Ln, Greensboro, NC 27407, USA
    ##   3700-3808 Frazier Rd, Greensboro, NC 27407, USA
    ##   Greensboro, NC 27407, USA
    ##   Morehead, NC, USA
    ##   Greensboro, NC, USA
    ##   Guilford County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.206604,-92.27300262&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   18 Morrison Ln, Norfork, AR 72658, USA
    ##   20 Hale Ln, Norfork, AR 72658, USA
    ##   14387 AR-5, Norfork, AR 72658, USA
    ##   Norfork, AR, USA
    ##   North Fork Township, AR, USA
    ##   Norfork, AR 72658, USA
    ##   Baxter County, AR, USA
    ##   Arkansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.23109436,-82.20570374&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   36950 Staff Ln, Zephyrhills, FL 33541, USA
    ##   36916 Staff Ln, Zephyrhills, FL 33541, USA
    ##   36900-36998 Marl Ave, Zephyrhills, FL 33541, USA
    ##   Zephyrhills West, FL, USA
    ##   Zephyrhills Colony Company, Zephyrhills, FL, USA
    ##   Zephyrhills, FL 33541, USA
    ##   Pasco County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.45489502,-90.9029007&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   26716 Palmetto Lake Ct W, Denham Springs, LA 70726, USA
    ##   11356 Palmetto Lake Ave, Denham Springs, LA 70726, USA
    ##   Palmetto Ct W, Denham Springs, LA 70726, USA
    ##   5, LA, USA
    ##   Denham Springs, LA 70726, USA
    ##   Livingston Parish, LA, USA
    ##   Louisiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.16239929,-118.1275024&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   970 N Wilson Ave, Pasadena, CA 91104, USA
    ##   McDonald Park, 1000 E Mountain St, Pasadena, CA 91104, USA
    ##   952 Mar Vista Ave, Pasadena, CA 91104, USA
    ##   Unnamed Road, Pasadena, CA 91104, USA
    ##   Bungalow Heaven, Pasadena, CA 91104, USA
    ##   Pasadena, CA 91104, USA
    ##   Pasadena, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.43930054,-111.7698975&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2831 E Gary St, Mesa, AZ 85213, USA
    ##   2819 E Gary St, Mesa, AZ 85213, USA
    ##   Northgrove, Mesa, AZ 85213, USA
    ##   Mesa, AZ 85213, USA
    ##   Mesa, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.90339661,-76.98819733&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1240 Morse St NE, Washington, DC 20002, USA
    ##   1235 Montello Ave NE, Washington, DC 20002, USA
    ##   1236 Morse St NE, Washington, DC 20002, USA
    ##   Trinidad, Washington, DC 20002, USA
    ##   Washington, DC 20002, USA
    ##   Washington, DC, USA
    ##   District of Columbia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.40769958,-82.44049835&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Stone Circle, 900 13th Ave, Huntington, WV 25701, USA
    ##   900 13th Ave, Huntington, WV 25701, USA
    ##   830 13th Ave, Huntington, WV 25701, USA
    ##   13th Ave, Huntington, WV 25701, USA
    ##   2, WV, USA
    ##   Huntington, WV, USA
    ##   Huntington, WV 25701, USA
    ##   Cabell County, WV, USA
    ##   West Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.19549561,-83.48940277&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   600 Sumpter Rd, Belleville, MI 48111, USA
    ##   64 Rose Blvd, Van Buren Charter Township, MI 48111, USA
    ##   31-49 Rose Blvd, Van Buren Charter Township, MI 48111, USA
    ##   Van Buren Charter Township, MI, USA
    ##   Belleville, MI 48111, USA
    ##   Wayne County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.75450134,-95.40930176&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2050 Brentwood Dr, Houston, TX 77019, USA
    ##   2055 Mellmeade Ct, Houston, TX 77019, USA
    ##   Montrose, Houston, TX, USA
    ##   Houston, TX 77019, USA
    ##   Houston, TX, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.70129395,-72.67630005&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   42 Knight St, Wethersfield, CT 06109, USA
    ##   41 Knight St, Wethersfield, CT 06109, USA
    ##   55-83 Bond St, Wethersfield, CT 06109, USA
    ##   Wethersfield, CT, USA
    ##   Wethersfield, CT 06109, USA
    ##   Hartford County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.6013031,-111.8867035&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9008 E Larkspur Dr, Scottsdale, AZ 85260, USA
    ##   9007 E Larkspur Dr, Scottsdale, AZ 85260, USA
    ##   12668 N 90th St, Scottsdale, AZ 85260, USA
    ##   N 90th St, Scottsdale, AZ 85260, USA
    ##   Country Trace, Scottsdale, AZ 85260, USA
    ##   Scottsdale, AZ 85260, USA
    ##   Scottsdale, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.79299927,-74.02469635&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5900 Tonnelle Ave, North Bergen, NJ 07047, USA
    ##   6115 Granton Ave, North Bergen, NJ 07047, USA
    ##   6107 Granton Ave, North Bergen, NJ 07047, USA
    ##   6131-6200 Grand Ave, North Bergen, NJ 07047, USA
    ##   North Bergen, NJ 07047, USA
    ##   North Bergen, NJ, USA
    ##   Hudson County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.73379517,-116.9299011&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   26745 Meridian St, Hemet, CA 92544, USA
    ##   41880 Johnston Ave, Hemet, CA 92544, USA
    ##   41982 Johnston Ave, Hemet, CA 92544, USA
    ##   Johnston Ave, Hemet, CA 92544, USA
    ##   East Hemet, CA, USA
    ##   Hemet, CA 92544, USA
    ##   Riverside County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=19.45010376,-70.69979858&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Parque Colon, Calle del Sol, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Calle del Sol 43, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Calle del Sol 52, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Calle del Sol 51, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Calle Cuba, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Centro Histórico de Santiago, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Los Pepines, Santiago De Los Caballeros 51000, Dominican Republic
    ##   Santiago De Los Caballeros, Dominican Republic
    ##   Santiago Province, Dominican Republic
    ##   51000, Dominican Republic
    ##   Dominican Republic
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.75819397,-88.29709625&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   200 Beach St, Aurora, IL 60505, USA
    ##   175 N State St, Aurora, IL 60505, USA
    ##   782 Claim St, Aurora, IL 60505, USA
    ##   224-200 Beach St, Aurora, IL 60505, USA
    ##   Aurora, IL 60505, USA
    ##   Aurora Township, IL, USA
    ##   Aurora, IL, USA
    ##   Kane County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.81159973,-81.49729919&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1201 Valerie Ave NE, Massillon, OH 44646, USA
    ##   2100 Carlyle St NW, Massillon, OH 44646, USA
    ##   1147 Valerie Ave NE, Massillon, OH 44646, USA
    ##   1400-1448 Valerie Ave NE, Massillon, OH 44646, USA
    ##   Massillon, OH, USA
    ##   Massillon, OH 44646, USA
    ##   Stark County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.36599731,-71.22709656&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   88 Cedar St, Waltham, MA 02453, USA
    ##   210 High St, Waltham, MA 02453, USA
    ##   250 High St, Waltham, MA 02453, USA
    ##   Unnamed Road, Waltham, MA 02453, USA
    ##   South Side, Waltham, MA 02453, USA
    ##   Waltham, MA 02453, USA
    ##   Waltham, MA, USA
    ##   Middlesex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10 Aldermanbury, London EC2V 7RF, UK
    ##   1 Love Ln, London EC2V, UK
    ##   Aldermanbury, London EC2V, UK
    ##   Love Ln, London EC2V 7JN, UK
    ##   London EC2V, UK
    ##   City of London, UK
    ##   City of London, London, UK
    ##   London, UK
    ##   Greater London, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.44670105,-82.020401&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2850 S Ridge Dr, Avon, OH 44011, USA
    ##   2830 Center Rd, Avon, OH 44011, USA
    ##   2827 Center Rd, Avon, OH 44011, USA
    ##   Avon, OH 44011, USA
    ##   Lorain County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.25019836,-94.37030029&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6245 Bonanza Rd, Fort Smith, AR 72916, USA
    ##   Mine 18 Rd, Fort Smith, AR 72916, USA
    ##   Marion Township, AR, USA
    ##   Fort Smith, AR 72916, USA
    ##   Sebastian County, AR, USA
    ##   Arkansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.81919861,-117.1002045&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4851 La Cuenta Dr, San Diego, CA 92124, USA
    ##   10854 Valldemosa Ln, San Diego, CA 92124, USA
    ##   4850 La Cuenta Dr, San Diego, CA 92124, USA
    ##   10998-10850 Valldemosa Ln, San Diego, CA 92124, USA
    ##   Tierrasanta, San Diego, CA 92124, USA
    ##   San Diego, CA 92124, USA
    ##   San Diego, CA, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   383 Washington St, Middletown, CT 06457, USA
    ##   Unnamed Road, Middletown, CT 06457, USA
    ##   Middletown, CT, USA
    ##   Middletown, CT 06457, USA
    ##   Middlesex County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.3309021,-89.48370361&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   16 Co Rd 4015, Oxford, MS 38655, USA
    ##   57 Co Rd 4015, Oxford, MS 38655, USA
    ##   Unnamed Road, Oxford, MS 38655, USA
    ##   Lafayette Springs, MS 38655, USA
    ##   Lafayette County, MS, USA
    ##   Mississippi, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.20759583,-87.18060303&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   301 KY-181, Greenville, KY 42345, USA
    ##   301 US-62, Greenville, KY 42345, USA
    ##   200-298 US-62, Greenville, KY 42345, USA
    ##   Greenville, KY, USA
    ##   Greenville, KY 42345, USA
    ##   Muhlenberg County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.30780029,-88.146698&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   110 S Third Suite B, Wilmington, IL 60481, United States
    ##   105 S Water St, Wilmington, IL 60481, USA
    ##   104 S Water St, Wilmington, IL 60481, USA
    ##   109 IL-53, Wilmington, IL 60481, USA
    ##   IL-53, Wilmington, IL 60481, USA
    ##   Wilmington, IL 60481, USA
    ##   Wilmington Township, IL, USA
    ##   Custer Park, IL 60481, USA
    ##   Will County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=48.85429382,2.352706909&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Hôtel de Ville, Quai de l'Hôtel de ville, 75004 Paris, France
    ##   11 Quai aux Fleurs, 75004 Paris, France
    ##   Voie Georges Pompidou, 75004 Paris, France
    ##   Notre Dame, Paris, France
    ##   4th arrondissement, 75004 Paris, France
    ##   75004 Paris, France
    ##   Paris, France
    ##   Île-de-France, France
    ##   France
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.19740295,-96.61769867&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   300 E Louisiana St, McKinney, TX 75069, USA
    ##   Dr. Glenn Mitchell Memorial Park, 300 W Louisiana St, McKinney, TX 75069, USA
    ##   301 W Louisiana St, McKinney, TX 75069, USA
    ##   303 W Louisiana St, McKinney, TX 75069, USA
    ##   Church St, McKinney, TX 75069, USA
    ##   Fairview, TX 75069, USA
    ##   McKinney, TX, USA
    ##   Collin County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.41409302,-93.87419891&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6495 Flournoy Lucas Rd, Shreveport, LA 71129, USA
    ##   Shreveport, LA 71129, USA
    ##   11, LA, USA
    ##   Caddo Parish, LA, USA
    ##   Louisiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-23.66799927,-46.52119446&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   R. Cel. Seabra, 214 - Vila Leopoldina, Santo André - SP, 09176-000, Brazil
    ##   R. Tancredo do Amaral, 2-94 - Vila Alzira, Santo André - SP, 09176-000, Brazil
    ##   R. Cel. Seabra, 225 - Vila Marina, Santo André - SP, 09176-000, Brazil
    ##   Unnamed Road - Vila Assunção, Santo André - SP, Brazil
    ##   Santo André - State of São Paulo, 09176-000, Brazil
    ##   Santo André - State of São Paulo, Brazil
    ##   Vila Assunção, Santo André - SP, Brazil
    ##   Santo André, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   2751 Silver Ridge Dr, Orlando, FL 32818, USA
    ##   2767 Silver Ridge Dr, Orlando, FL 32818, USA
    ##   2762 Silver Ridge Dr, Orlando, FL 32818, USA
    ##   Orlando, FL 32818, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.13969421,-86.51409912&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2750 S Wexley Rd, Bloomington, IN 47401, USA
    ##   Unnamed Road, Bloomington, IN 47401, USA
    ##   Bloomington, IN, USA
    ##   Perry Township, IN, USA
    ##   Bloomington, IN 47401, USA
    ##   Monroe County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.60049438,-83.62509918&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2150 S Byrne Rd, Toledo, OH 43614, USA
    ##   2042 S Byrne Rd, Toledo, OH 43614, USA
    ##   2040 S Byrne Rd, Toledo, OH 43614, USA
    ##   Byrne & Glanzman SE, Toledo, OH 43614, USA
    ##   2116 S Byrne Rd, Toledo, OH 43614, USA
    ##   2145-2121 S Byrne Rd, Toledo, OH 43614, USA
    ##   Glendale-Heatherdowns, Toledo, OH, USA
    ##   Toledo, OH 43614, USA
    ##   Toledo, OH, USA
    ##   Lucas County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-23.49830627,-46.86509705&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Multiple addresses found, the first will be returned:
    ##   Av. Antonio Furlan, 488 - Vila Boa Vista, Barueri - SP, 06414-065, Brazil
    ##   Rua Claudino de Oliveira Pessoa, 645-707 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Dr. Dib Sauaia Neto, 983 - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Av. Sebastião Davino dos Réis - Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Alphaville Res. Dois, Barueri - SP, Brazil
    ##   Barueri - State of São Paulo, Brazil
    ##   Barueri, SP, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.58850098,-75.46420288&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1202-1206 S 6th St, Allentown, PA 18103, USA
    ##   Park Rd, Allentown, PA 18103, USA
    ##   1299 S 7th St, Allentown, PA 18103, USA
    ##   Allentown, PA 18103, USA
    ##   Allentown, PA, USA
    ##   Lehigh County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.17120361,-91.88950348&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   600 W Jackson St, Mexico, MO 65265, USA
    ##   627 State Hwy FF, Mexico, MO 65265, USA
    ##   716-638 State Hwy FF, Mexico, MO 65265, USA
    ##   Mexico, MO 65265, USA
    ##   Salt River Township, MO 65265, USA
    ##   Audrain County, MO, USA
    ##   Missouri, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=25.78059387,-80.18260193&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Port Miami Bridge, Port Blvd, Miami, FL 33132, USA
    ##   1120 Port Blvd, Miami, FL 33132, USA
    ##   1017 NE 6th St, Miami, FL 33132, USA
    ##   901 S America Way, Miami, FL 33132, USA
    ##   NE 6th St, Miami, FL 33132, USA
    ##   FRS Caribbean, 901 S America Way, Miami, FL 33132, USA
    ##   Miami, FL 33132, USA
    ##   Downtown Miami, Miami, FL, USA
    ##   Miami, FL, USA
    ##   Miami-Dade County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ware Housing Corporation Road, Opposite South Railway Station, Ernakulam South, Kochi, Kerala 682016, India
    ##   2757a, Kalathiparambu Rd, Near, Ernakulam South, Kochi, Kerala 682016, India
    ##   Kalathiparambu Cross Rd, Kalathiparambil, Ernakulam South, Ernakulam, Kerala 682016, India
    ##   Kalathiparambil, Ernakulam South, Kochi, Kerala 682016, India
    ##   Valanjambalam, Kochi, Kerala 682016, India
    ##   Kochi, Kerala 682016, India
    ##   Ernakulam, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.00880432,-75.67569733&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   141 Bayberry Rd, Kill Devil Hills, NC 27948, USA
    ##   142 Bayberry Rd, Kill Devil Hills, NC 27948, USA
    ##   145 Partridge Trail, Kill Devil Hills, NC 27948, USA
    ##   Partridge Trail, Kill Devil Hills, NC 27948, USA
    ##   Kill Devil Hills, NC 27948, USA
    ##   Atlantic, NC, USA
    ##   Dare County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.706604,-74.20269775&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   578 Elizabeth Ave, Newark, NJ 07112, USA
    ##   1 Lehigh Ave, Newark, NJ 07112, USA
    ##   Elizabeth Ave at Lehigh Ave, Newark, NJ 07112, USA
    ##   567 Elizabeth Ave, Newark, NJ 07112, USA
    ##   Weequahic Park, Elizabeth Ave &, Meeker Ave, Newark, NJ 07112, United States
    ##   Dayton/Weequahic Park, Newark, NJ, USA
    ##   Newark, NJ 07112, USA
    ##   Newark, NJ, USA
    ##   Essex County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.70120239,-79.38770294&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   220 Davisville Ave, Toronto, ON M4S, Canada
    ##   506 Mt Pleasant Rd, Toronto, ON M4S, Canada
    ##   501 Mt Pleasant Rd, Toronto, ON M4S 2L9, Canada
    ##   497 Mt Pleasant Rd, Toronto, ON M4S, Canada
    ##   520-508 Mt Pleasant Rd, Toronto, ON M4S 2M2, Canada
    ##   Mount Pleasant West, Toronto, ON, Canada
    ##   Toronto, ON M4S, Canada
    ##   Davisville Village, Toronto, ON, Canada
    ##   Old Toronto, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.89039612,12.5124054&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Via Statilia Park, Via Statilia, 00185 Roma RM, Italy
    ##   Via S. Croce In Gerusalemme/Statilia, 00185 Roma RM, Italy
    ##   Via Statilia, 21, 00185 Roma RM, Italy
    ##   Via di S. Croce in Gerusalemme, 38, 00185 Roma RM, Italy
    ##   Via Statilia, 00185 Roma RM, Italy
    ##   Esquilino, Rome, Metropolitan City of Rome, Italy
    ##   00185 Rome, Metropolitan City of Rome, Italy
    ##   Municipio I, Rome, Metropolitan City of Rome, Italy
    ##   Rome, Metropolitan City of Rome, Italy
    ##   Metropolitan City of Rome, Italy
    ##   Lazio, Italy
    ##   Italy
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.54359436,-81.37380219&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   105 N Rosalind Ave, Orlando, FL 32801, USA
    ##   309 E Central Blvd, Orlando, FL 32801, USA
    ##   Unnamed Road, Orlando, FL 32801, USA
    ##   South Eola, Orlando, FL 32801, USA
    ##   Lake Eola Park, 512 E Washington St, Orlando, FL 32801, USA
    ##   Lake Eola Heights, Orlando, FL, USA
    ##   Orlando, FL 32801, USA
    ##   Orlando, FL, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   451, Naya Mohalla, Ludhiana, Punjab 141008, India
    ##   Unnamed Road, Naya Mohalla, Ludhiana, Punjab 141008, India
    ##   Naya Mohalla, Ludhiana, Punjab 141008, India
    ##   Punjab 141008, India
    ##   Ludhiana, Punjab, India
    ##   Punjab, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.49650574,-80.20600128&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   500 Cherrington Pkwy, Moon, PA 15108, USA
    ##   500 Corporate Center Dr, Moon, PA 15108, USA
    ##   500 Cherrington Parkway Ste. 300 Moon Township, Moon, PA 15108, United States
    ##   304 Cherrington Pkwy, Moon, PA 15108, USA
    ##   351-325 Cherrington Pkwy, Moon, PA 15108, USA
    ##   Moon, PA, USA
    ##   Moon, PA 15108, USA
    ##   Allegheny County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.76089478,-73.91149902&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   45-02 30th Rd, Long Island City, NY 11103, USA
    ##   30-38 45th St, Astoria, NY 11103, USA
    ##   45th St, Astoria, NY 11103, USA
    ##   Long Island City, NY 11103, USA
    ##   Astoria, Queens, NY, USA
    ##   Queens, NY, USA
    ##   Queens County, Queens, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.08810425,-74.11949921&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   401 Central Blvd E, Brick Township, NJ 08724, USA
    ##   Central Blvd E, Brick Township, NJ 08724, USA
    ##   Brick Township, NJ 08724, USA
    ##   Brick Township, NJ, USA
    ##   Ocean County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.60549927,-84.77960205&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   320 W Broadway St, Mt Pleasant, MI 48858, USA
    ##   S Island Park Dr, Mt Pleasant, MI 48858, USA
    ##   Mt Pleasant, MI 48858, USA
    ##   Isabella County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.97709656,-75.90930176&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   122 Newell St, Watertown, NY 13601, USA
    ##   136 Newell St, Watertown, NY 13601, USA
    ##   100-132 Newell St, Watertown, NY 13601, USA
    ##   Watertown, NY 13601, USA
    ##   Jefferson County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.7026062,-98.47589874&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   27631 Papoose Pass, San Antonio, TX 78260, USA
    ##   San Antonio, TX 78260, USA
    ##   Far North Central, San Antonio, TX, USA
    ##   San Antonio, TX, USA
    ##   Bexar County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.45379639,-81.4673996&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1 Canada Ave, Orlando, FL 32819, USA
    ##   Unnamed Road, Orlando, FL 32819, USA
    ##   Orlando, FL 32819, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.61399841,-104.9601974&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Cherryville Park, 5711 S University Blvd, Greenwood Village, CO 80121, USA
    ##   5711 S University Blvd, Greenwood Village, CO 80121, USA
    ##   2355 Cherryville Rd, Greenwood Village, CO 80121, USA
    ##   S University Blvd & Cherryville Rd, Greenwood Village, CO 80121, USA
    ##   5753 CO-177, Greenwood Village, CO 80121, USA
    ##   S University Blvd, Greenwood Village, CO 80121, USA
    ##   Littleton, CO 80121, USA
    ##   Greenwood Village, CO, USA
    ##   Arapahoe County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.33599854,-84.31259918&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7076 Mason Montgomery Rd, Mason, OH 45040, USA
    ##   723 Western Row Rd, Mason, OH 45040, USA
    ##   Western Row Rd & Mason-Montgomery, Mason, OH 45040, USA
    ##   7097 Mason Montgomery Rd, Mason, OH 45040, USA
    ##   Mason Montgomery Rd, Mason, OH 45040, USA
    ##   Mason, OH, USA
    ##   Mason, OH 45040, USA
    ##   Warren County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=12.25,109.1832886&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   272 Th<U+1ED1>ng Nh<U+1EA5>t, Phuong son, Thành ph<U+1ED1> Nha Trang, Khánh Hòa 650000, Vietnam
    ##   272b Th<U+1ED1>ng Nh<U+1EA5>t, Phuong son, Thành ph<U+1ED1> Nha Trang, Khánh Hòa 650000, Vietnam
    ##   272 QL1C, Phuong son, Thành ph<U+1ED1> Nha Trang, Khánh Hòa 650000, Vietnam
    ##   QL1C, Phuong son, Thành ph<U+1ED1> Nha Trang, Khánh Hòa 650000, Vietnam
    ##   Phuong Son, Tp. Nha Trang, Khánh Hòa 650000, Vietnam
    ##   Phuong Son, Thành ph<U+1ED1> Nha Trang, Khanh Hoa Province 650000, Vietnam
    ##   Nha Trang, Khanh Hoa Province 650000, Vietnam
    ##   Thành ph<U+1ED1> Nha Trang, Khánh Hòa, Vietnam
    ##   Nha Trang, Khanh Hoa Province, Vietnam
    ##   Khanh Hoa Province, Vietnam
    ##   Vietnam
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.17829895,-80.27339935&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9300 NW 43rd St, Sunrise, FL 33351, USA
    ##   9220 NW 44th St, Sunrise, FL 33351, USA
    ##   9235 NW 44th St, Sunrise, FL 33351, USA
    ##   9368-9250 NW 44th St, Sunrise, FL 33351, USA
    ##   Fort Lauderdale, FL 33351, USA
    ##   Sunrise, FL, USA
    ##   Broward County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=27.94619751,-82.46070099&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   200N N Ashley Dr, Tampa, FL 33602, USA
    ##   200 N Ashley Dr, Tampa, FL 33602, USA
    ##   19 W Kennedy Blvd, Tampa, FL 33606, USA
    ##   199 FL-685, Tampa, FL 33602, USA
    ##   19 FL-685, Tampa, FL 33606, USA
    ##   Tampa, FL 33606, USA
    ##   Northwest Tampa, Tampa, FL, USA
    ##   Tampa, FL, USA
    ##   Hillsborough County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.56619263,-72.34410095&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   208 Taintor Hill Rd, Colchester, CT 06415, USA
    ##   Taintor Hill Rd, Colchester, CT 06415, USA
    ##   Colchester Center, Colchester, CT 06415, USA
    ##   Colchester, CT 06415, USA
    ##   New London County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Mississauga, ON L5V 0B6, Canada
    ##   Mississauga, ON L5V, Canada
    ##   East Credit, Mississauga, ON, Canada
    ##   Mississauga, ON, Canada
    ##   Regional Municipality of Peel, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.97099304,-93.04979706&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1020 Duluth St, St Paul, MN 55106, USA
    ##   1034 Duluth St, St Paul, MN 55106, USA
    ##   1118-1200 Jenks Ave E, St Paul, MN 55106, USA
    ##   Payne - Phalen, St Paul, MN, USA
    ##   St Paul, MN 55106, USA
    ##   St Paul, MN, USA
    ##   Ramsey County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.71870422,-97.75330353&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   409 W Majestic Oak Ln, Georgetown, TX 78633, USA
    ##   407 W Majestic Oak Ln, Georgetown, TX 78633, USA
    ##   409-405 Sunset Ridge, Georgetown, TX 78633, USA
    ##   Georgetown, TX 78633, USA
    ##   Williamson County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.14399719,-90.04799652&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   240 Madison Ave, Memphis, TN 38103, USA
    ##   255 Madison Ave, Memphis, TN 38103, USA
    ##   Madison Ave, Memphis, TN 38103, USA
    ##   Downtown Memphis, Memphis, TN, USA
    ##   Memphis, TN 38103, USA
    ##   Memphis, TN, USA
    ##   Shelby County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.71240234,-79.36440277&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   220 Laird Dr, East York, ON M4G 3X2, Canada
    ##   Laird Dr At Vanderhoof Ave, Toronto, ON M4G 2H4, Canada
    ##   111 Parklea Dr, East York, ON M4G 2J9, Canada
    ##   220 Laird Dr, Toronto, ON M4G, Canada
    ##   81-117 Parklea Dr, East York, ON M4G 2J9, Canada
    ##   East York, ON M4G 3X2, Canada
    ##   Leaside, Toronto, ON, Canada
    ##   North York, ON M4G, Canada
    ##   East York, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.04089355,-84.0236969&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   343 Old Peachtree Rd NE, Lawrenceville, GA 30043, USA
    ##   Unnamed Road, Suwanee, GA 30024, USA
    ##   Suwanee, GA 30024, USA
    ##   Gwinnett County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.27890015,-85.69039917&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7233 W Kl Ave, Kalamazoo, MI 49009, USA
    ##   7095 W Kl Ave, Kalamazoo, MI 49009, USA
    ##   1076 S 8th St, Kalamazoo, MI 49009, USA
    ##   800-1058 S 8th St, Kalamazoo, MI 49009, USA
    ##   Oshtemo Township, MI, USA
    ##   Kalamazoo, MI 49009, USA
    ##   Kalamazoo County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.48100281,-71.15630341&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   21 Harrison Ave, Woburn, MA 01801, USA
    ##   25 Harrison Ave, Woburn, MA 01801, USA
    ##   20 Harrison Ave, Woburn, MA 01801, USA
    ##   Abbott St, Woburn, MA 01801, USA
    ##   Woburn, MA 01801, USA
    ##   Woburn, MA, USA
    ##   Middlesex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.82060242,-118.0339966&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9740 Graham St, Cypress, CA 90630, USA
    ##   9702 Graham St, Cypress, CA 90630, USA
    ##   Oak Knoll Park, 9600 Graham St, Cypress, CA 90630, USA
    ##   9735 Graham St, Cypress, CA 90630, USA
    ##   9810-9736 Graham St, Cypress, CA 90630, USA
    ##   Cypress, CA 90630, USA
    ##   Cypress, CA, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.82850647,-81.32369995&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   120 Allgood Cir, St Augustine Beach, FL 32086, USA
    ##   113 Allgood Cir, St. Augustine, FL 32086, USA
    ##   Unnamed Road, United States
    ##   ST AUG BEACH, FL 32086, USA
    ##   St Johns County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.88699341,-78.521698&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1015 W Spring St, Woodstock, VA 22664, USA
    ##   1000 State Rte 816, Woodstock, VA 22664, USA
    ##   1099-1001 State Rte 816, Woodstock, VA 22664, USA
    ##   Woodstock, VA 22664, USA
    ##   District 4, VA, USA
    ##   Shenandoah County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.97329712,-84.22309875&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5445 Triangle Pkwy NW, Norcross, GA 30092, USA
    ##   Triangle Pkwy & Triangle Drive OB, Peachtree Corners, GA 30092, USA
    ##   5335 Data Dr, Norcross, GA 30092, USA
    ##   5510 Triangle Pkwy NW, Norcross, GA 30092, USA
    ##   Peachtree Corners, GA 30092, USA
    ##   Peachtree Corners, GA, USA
    ##   Gwinnett County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Computer Science, Loop Rd, Staten Island, NY 10314, USA
    ##   Loop Rd, Staten Island, NY 10314, USA
    ##   Staten Island, NY 10314, USA
    ##   Mid Island, Staten Island, NY, USA
    ##   Richmond County, Staten Island, NY, USA
    ##   Staten Island, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1/A, Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka 560001, India
    ##   Unnamed Road, Ambedkar Veedhi, Bengaluru, Karnataka 560001, India
    ##   Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka, India
    ##   Bengaluru, Karnataka 560001, India
    ##   Bengaluru, Karnataka, India
    ##   Bangalore Urban, Karnataka, India
    ##   Karnataka, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.26919556,-80.16110229&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   140 Morganza Rd, Canonsburg, PA 15317, USA
    ##   400 Southpointe Blvd, Canonsburg, PA 15317, USA
    ##   Morganza Rd, Canonsburg, PA 15317, USA
    ##   North Strabane Township, PA, USA
    ##   Canonsburg, PA 15317, USA
    ##   Washington County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.43940735,-75.84649658&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   ARRÊT DE COURTOISIE Pink/Klock, Gatineau, QC J9J 3G9, Canada
    ##   Chemin Pink, Gatineau, QC J9J, Canada
    ##   1301 Chemin Pink, Gatineau, QC J9J, Canada
    ##   1501 Chemin Pink, Gatineau, QC J9J 3N5, Canada
    ##   Gatineau, QC J9J 3G9, Canada
    ##   District de Deschenes, Gatineau, QC, Canada
    ##   Gatineau, QC J9J, Canada
    ##   Gatineau, QC, Canada
    ##   Communauté-Urbaine-de-l'Outaouais, QC, Canada
    ##   Quebec, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.94850159,-75.95649719&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   85 N Wilson St, Hazleton, PA 18201, USA
    ##   89 N Wilson St, Hazleton, PA 18201, USA
    ##   Cemetery Rd, Hazleton, PA 18201, USA
    ##   Hazleton, PA, USA
    ##   Hazle Township, PA 18201, USA
    ##   Luzerne County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.62269592,-86.24520111&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   301-499 Jackson Rd, South Bend, IN 46614, USA
    ##   373 Jackson Rd, South Bend, IN 46614, USA
    ##   Fellows St, South Bend, IN 46614, USA
    ##   Centre Township, IN, USA
    ##   South Bend, IN, USA
    ##   South Bend, IN 46614, USA
    ##   St Joseph County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.64030457,-79.37110138&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   39 Queens Quay E, Toronto, ON M5A 1B6, Canada
    ##   25 R Queens Quay E, Toronto, ON M5E 0A4, Canada
    ##   29 Queens Quay E, Toronto, ON M5E 0A4, Canada
    ##   Unnamed Road, Toronto, ON M5E 0A4, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.00480652,-86.78859711&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   314 Mint Spring Cir, Brentwood, TN 37027, USA
    ##   910 Heritage Way, Brentwood, TN 37027, USA
    ##   315 Mint Spring Cir, Brentwood, TN 37027, USA
    ##   Heritage Way, Brentwood, TN 37027, USA
    ##   900 Heritage Way, Brentwood, TN 37027, USA
    ##   Brentwood, TN, USA
    ##   Brentwood, TN 37027, USA
    ##   Williamson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   12608 Bella Pkwy, Manor, TX 78653, USA
    ##   12691 Old Hwy 20, Manor, TX 78653, USA
    ##   Bella Pkwy, Manor, TX 78653, USA
    ##   Webberville, TX 78653, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1708 Blvd Napoleon, Louisville, KY 40205, USA
    ##   Hal Warheim Park, 1832 Overlook Terrace, Louisville, KY 40205, USA
    ##   2424 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   2419 Boulevard Napoleon, Louisville, KY 40205, USA
    ##   1899-1883 Overlook Terrace, Louisville, KY 40205, USA
    ##   Belknap, Louisville, KY 40205, USA
    ##   STRATHMR MNR, KY 40205, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.68829346,-71.15740204&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   151 Foster St, Fall River, MA 02721, USA
    ##   Warren Street and Foster Street, Fall River, MA 02721, USA
    ##   32 Richmond St, Fall River, MA 02721, USA
    ##   Fall River, MA 02721, USA
    ##   Fall River, MA, USA
    ##   Bristol County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.08180237,-82.96649933&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1860 Walden Dr, Columbus, OH 43229, USA
    ##   1913 Brookfield Rd, Columbus, OH 43229, USA
    ##   5639-5599 Beechcroft Rd, Columbus, OH 43229, USA
    ##   Forest Park East, Columbus, OH, USA
    ##   Columbus, OH 43229, USA
    ##   Columbus, OH, USA
    ##   Franklin County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.17730713,-105.1008987&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1050 Kimbark St, Longmont, CO 80501, USA
    ##   440 11th Ave, Longmont, CO 80501, USA
    ##   1053 Kimbark St, Longmont, CO 80501, USA
    ##   1199-1101 Kimbark St, Longmont, CO 80501, USA
    ##   Kiteley, Longmont, CO 80501, USA
    ##   Longmont, CO 80501, USA
    ##   Longmont, CO, USA
    ##   Boulder County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.23190308,-84.16269684&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1 Barker Rd, Cumming, GA 30040, USA
    ##   78 Tower Rd, Cumming, GA 30040, USA
    ##   Unnamed Road, Cumming, GA 30040, USA
    ##   Cumming, GA 30040, USA
    ##   Forsyth County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=51.74819946,-0.432601929&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   The Leather Bottle PH, Hemel Hempstead HP2 4PZ, UK
    ##   109 Leverstock Green Way, Hemel Hempstead HP3 8QE, UK
    ##   109 A4147, Hemel Hempstead HP3 8QE, UK
    ##   A4147, Hemel Hempstead HP3 8QE, UK
    ##   Hemel Hempstead HP2 4PZ, UK
    ##   Hemel Hempstead, UK
    ##   Hemel Hempstead HP3, UK
    ##   Dacorum District, UK
    ##   Hertfordshire, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.08279419,-88.02690125&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3513 N 91st St, Milwaukee, WI 53222, USA
    ##   3519 N 91st St, Milwaukee, WI 53222, USA
    ##   3540 N 92nd St, Milwaukee, WI 53222, USA
    ##   3515 N 91st St, Milwaukee, WI 53222, USA
    ##   9199-9101 W Keefe Ave, Milwaukee, WI 53222, USA
    ##   Kops Park, Milwaukee, WI 53222, USA
    ##   Milwaukee, WI 53222, USA
    ##   Milwaukee, WI, USA
    ##   Milwaukee County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.47659302,-96.7052002&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7301 Cliff Ave, Sioux Falls, SD 57108, USA
    ##   47510 85th St, Sioux Falls, SD 57108, USA
    ##   26991 Cliff Ave, Sioux Falls, SD 57108, USA
    ##   27026-27000 Co Hwy 123, Sioux Falls, SD 57108, USA
    ##   Springdale Township, SD, USA
    ##   Sioux Falls, SD 57108, USA
    ##   Lincoln County, SD, USA
    ##   South Dakota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   734, RB Kumthekar Rd, Perugate, Sadashiv Peth, Pune, Maharashtra 411030, India
    ##   664, RB Kumthekar Rd, Perugate, Sadashiv Peth, Pune, Maharashtra 411030, India
    ##   Unnamed Road, Perugate, Sadashiv Peth, Pune, Maharashtra 411030, India
    ##   Sadashiv Peth, Pune, Maharashtra, India
    ##   Pune, Maharashtra 411030, India
    ##   Pune, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.43690491,-122.7126999&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   171 Santa Rosa Ave, Santa Rosa, CA 95404, USA
    ##   Prince Memorial Greenway, Santa Rosa, CA 95401, USA
    ##   Santa Rosa, CA 95401, USA
    ##   Santa Rosa, CA, USA
    ##   Sonoma County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.7993927,-117.1685944&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3002 Armstrong St, San Diego, CA 92111, USA
    ##   6948 Park Mesa Way, San Diego, CA 92111, USA
    ##   Ciota's Way, San Diego, CA 92111, USA
    ##   Linda Vista, San Diego, CA, USA
    ##   San Diego, CA 92111, USA
    ##   San Diego, CA, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.92900085,-89.22399902&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   416 Hyland Dr, Stoughton, WI 53589, USA
    ##   400 Hyland Dr, Stoughton, WI 53589, USA
    ##   1030 N Page St, Stoughton, WI 53589, USA
    ##   418 Hyland Dr, Stoughton, WI 53589, USA
    ##   421-401 Clancey Ln, Stoughton, WI 53589, USA
    ##   Stoughton, WI 53589, USA
    ##   Dane County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.76280212,-86.53430176&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   180 Urban St, Danville, IN 46122, USA
    ##   109 Spring St, Danville, IN 46122, USA
    ##   Spring St, Danville, IN 46122, USA
    ##   Danville, IN 46122, USA
    ##   Center Township, IN, USA
    ##   Hendricks County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.80540466,-104.740799&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4540 Fenton Rd, Colorado Springs, CO 80916, USA
    ##   1822 Harley Ln, Colorado Springs, CO 80916, USA
    ##   4562 Fenton Rd, Colorado Springs, CO 80916, USA
    ##   Fenton Rd, Colorado Springs, CO 80916, USA
    ##   Colorado Springs, CO 80916, USA
    ##   Colorado Springs, CO, USA
    ##   El Paso County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.18460083,-76.30149841&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1012 Elbow Rd, Lititz, PA 17543, USA
    ##   1017 Elbow Rd, Lititz, PA 17543, USA
    ##   114-198 Ashley Dr, Lititz, PA 17543, USA
    ##   Warwick Township, PA, USA
    ##   Lititz, PA 17543, USA
    ##   Lancaster County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.36650085,-73.97360229&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1091 Rue du Suroît, Pincourt, QC J7W 0A9, Canada
    ##   1074 Rue du Suroît, Pincourt, QC J7W 0A9, Canada
    ##   1401-1421 Rue des Lauriers, Pincourt, QC J7W 0A9, Canada
    ##   Pincourt, QC J7W 0A9, Canada
    ##   Pincourt, QC, Canada
    ##   Pincourt, QC J7W, Canada
    ##   Vaudreuil-Soulanges Regional County Municipality, QC, Canada
    ##   Quebec, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.76089478,-80.10939789&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   180 Tomlinson Drive, Zelienople, PA 16063, USA
    ##   153 Tomlinson Drive, Zelienople, PA 16063, USA
    ##   180 Tomlinson Dr, Zelienople, PA 16063, USA
    ##   Tomlinson Dr, Zelienople, PA 16063, USA
    ##   Zelienople, PA 16063, USA
    ##   Jackson Township, PA, USA
    ##   Butler County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.1598053,-95.74019623&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   28222 Eagle Cove, Magnolia, TX 77355, USA
    ##   28203 Eagle Cove, Magnolia, TX 77355, USA
    ##   28217 Eagle Cove, Magnolia, TX 77355, USA
    ##   Stagecoach, TX 77355, USA
    ##   Montgomery County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.83650208,-95.43630219&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1520 Candlelight Ln, Houston, TX 77018, USA
    ##   Candlelight Park and Community Center, 1520 Candlelight Ln, Houston, TX 77018, USA
    ##   4951 Oak Forest Dr, Houston, TX 77018, USA
    ##   5049-5001 Oak Forest Dr, Houston, TX 77018, USA
    ##   Houston, TX 77018, USA
    ##   Central Northwest, Houston, TX, USA
    ##   Houston, TX, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.07040405,-78.90670013&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8001 13th St, Waynesboro, VA 22980, USA
    ##   332 Rosser Ave, Waynesboro, VA 22980, USA
    ##   402 Rosser Ave, Waynesboro, VA 22980, USA
    ##   8007-8001 13th St, Waynesboro, VA 22980, USA
    ##   Waynesboro, VA 22980, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.7059021,-81.1996994&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6070 Conley Rd, Painesville, OH 44077, USA
    ##   6711-6071 Conley Rd, Painesville, OH 44077, USA
    ##   Concord Township, OH, USA
    ##   Painesville, OH 44077, USA
    ##   Lake County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.32829285,-86.48960114&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   713 5th St NE, Arab, AL 35016, USA
    ##   784 5th St NE, Arab, AL 35016, USA
    ##   724-776 5th St NE, Arab, AL 35016, USA
    ##   Arab, AL 35016, USA
    ##   Marshall County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   12279 Capital Blvd, Wake Forest, NC 27587, USA
    ##   12400 Wake Union Church Rd, Wake Forest, NC 27587, USA
    ##   12517 US-1, Wake Forest, NC 27587, USA
    ##   US-1, Wake Forest, NC 27587, USA
    ##   Wake Forest, NC 27587, USA
    ##   Wake Forest, NC, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.32020569,-84.55200195&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5866 Morningside Dr, Fairfield, OH 45014, USA
    ##   Point Pleasant Park, 2001 Resor Rd, Fairfield, OH 45014, USA
    ##   5872 Morningside Dr, Fairfield, OH 45014, USA
    ##   5801-5899 Judy Dr, Fairfield, OH 45014, USA
    ##   Fairfield, OH, USA
    ##   Hamilton, OH 45014, USA
    ##   Butler County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.67390442,-73.93579865&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   164 Troy Ave, Brooklyn, NY 11213, USA
    ##   238 Troy Ave, Brooklyn, NY 11213, USA
    ##   159 Troy Ave, Brooklyn, NY 11213, USA
    ##   173-171 Troy Ave, Brooklyn, NY 11213, USA
    ##   Brooklyn, NY 11213, USA
    ##   Crown Heights, Brooklyn, NY, USA
    ##   Brooklyn, NY, USA
    ##   Kings County, Brooklyn, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.6217041,-121.7935028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Eucalyptus Rd, Seaside, CA 93955, USA
    ##   2900 Parker Flats Cut Off Rd, Seaside, CA 93955, USA
    ##   Seaside, CA 93955, USA
    ##   Monterey County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=25.90919495,-80.3927002&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   14217 N Okeechobee Rd, Hialeah, FL 33018, USA
    ##   FL-25, Hialeah, FL 33018, USA
    ##   Hialeah, FL 33018, USA
    ##   Miami-Dade County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.7263031,-73.98179626&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Tompkins Square Park, E 10th St, New York, NY 10009, USA
    ##   144 Avenue A, New York, NY 10009, USA
    ##   Unnamed Road, New York, NY 10009, USA
    ##   Alphabet City, New York, NY 10009, USA
    ##   New York, NY 10009, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.00979614,-90.16300201&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3911 Hessmer Ave, Metairie, LA 70002, USA
    ##   3913 Hessmer Ave, Metairie, LA 70002, USA
    ##   Metairie, LA 70002, USA
    ##   Metairie, LA, USA
    ##   5, LA, USA
    ##   Jefferson Parish, LA, USA
    ##   Louisiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.75970459,-96.65419769&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5439 S 48th St, Lincoln, NE 68516, USA
    ##   Helen Boosalis Trail, Lincoln, NE 68516, USA
    ##   Lincoln, NE 68516, USA
    ##   Lincoln, NE, USA
    ##   Lancaster County, NE, USA
    ##   Nebraska, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.24620056,-83.6548996&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   759 Co Rd 479, Norman Park, GA 31771, USA
    ##   1067-761 Co Rd 479, Norman Park, GA 31771, USA
    ##   Norman Park, GA 31771, USA
    ##   Colquitt County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.00650024,-97.84059906&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Killeen, TX 76549, USA
    ##   Killeen, TX 76549, USA
    ##   Bell County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.57839966,-98.27510071&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   900 Ave J, Marble Falls, TX 78654, USA
    ##   1002 9th St, Marble Falls, TX 78654, USA
    ##   1004 9th St, Marble Falls, TX 78654, USA
    ##   9th St, Marble Falls, TX 78654, USA
    ##   Marble Falls, TX 78654, USA
    ##   Highland Haven, TX 78654, USA
    ##   Burnet County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.34590149,-121.2662964&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9300 Rices Texas Hill Rd, Oregon House, CA 95962, USA
    ##   9288 Rices Texas Hill Rd, Oregon House, CA 95962, USA
    ##   9287 Rices Texas Hill Rd, Oregon House, CA 95962, USA
    ##   Whitman Way, Oregon House, CA 95962, USA
    ##   Oregon House, CA 95962, USA
    ##   Yuba County, CA, USA
    ##   Sierra Nevada, California, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.01339722,-115.2077026&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4850 W Silverado Ranch Blvd, Las Vegas, NV 89141, USA
    ##   9700 S Decatur Blvd, Las Vegas, NV 89139, USA
    ##   4959-4901 W Silverado Ranch Blvd, Las Vegas, NV 89139, USA
    ##   Las Vegas, NV 89139, USA
    ##   Enterprise, NV, USA
    ##   Las Vegas, NV, USA
    ##   Clark County, NV, USA
    ##   Nevada, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=23.34779358,85.33859253&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   DS 88/B, Panchwati, Railway Colony, Gosaintola, Ranchi, Jharkhand 834001, India
    ##   Unnamed Road, Panchwati, Railway Colony, Gosaintola, Ranchi, Jharkhand 834001, India
    ##   Panchwati, Railway Colony, Gosaintola, Ranchi, Jharkhand 834001, India
    ##   Railway Colony, Gosaintola, Ranchi, Jharkhand 834001, India
    ##   Gosaintola, Ranchi, Jharkhand, India
    ##   Ranchi, Jharkhand 834001, India
    ##   Ranchi, Jharkhand, India
    ##   Jharkhand, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.855896,-70.93669891&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2 Keyser Lane, Amesbury, MA 01913, USA
    ##   98 Friend St, Amesbury, MA 01913, USA
    ##   2 Keyser Ln, Amesbury, MA 01913, USA
    ##   Amesbury, MA, USA
    ##   Amesbury, MA 01913, USA
    ##   Essex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.4190979,-87.77480316&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Harlem Ave, Monee, IL 60449, United States
    ##   6610 Lakeview Ln, Monee, IL 60449, USA
    ##   6567 W Lakeway Dr, Monee, IL 60449, USA
    ##   6699-6519 Lakeview Ln, Monee, IL 60449, USA
    ##   Monee, IL 60449, USA
    ##   Monee Township, IL, USA
    ##   Will County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=61.20489502,-149.8096008&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1750 Bragaw St, Anchorage, AK 99508, USA
    ##   1650 Bragaw St, Anchorage, AK 99508, USA
    ##   1740 Bragaw St, Anchorage, AK 99508, USA
    ##   Bragaw St, Anchorage, AK 99508, USA
    ##   Airport Heights Community Council, Anchorage, AK, USA
    ##   Anchorage, AK 99508, USA
    ##   Anchorage, AK, USA
    ##   Alaska, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.64959717,-71.92669678&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   36 Cobb Rd, Ashburnham, MA 01430, USA
    ##   122 Lake Rd, Ashburnham, MA 01430, USA
    ##   Unnamed Road, Ashburnham, MA 01430, USA
    ##   Ashburnham, MA 01430, USA
    ##   Ashburnham, MA, USA
    ##   Worcester County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.83509827,-117.8652039&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2916 Lincoln Ave, Anaheim, CA 92806, USA
    ##   (primarily covering ORANGE and neighboring counties), Anaheim, CA 92806, United States
    ##   2999 E Lincoln Ave, Anaheim, CA 92806, USA
    ##   Anaheim Coves Trail, Anaheim, CA 92806, USA
    ##   Southeast Anaheim, Anaheim, CA, USA
    ##   Anaheim, CA 92806, USA
    ##   Anaheim, CA, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.55299377,-81.7193985&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   242 Ray Ln, Aiken, SC 29801, USA
    ##   247 Ray Ln, Aiken, SC 29801, USA
    ##   248 Ray Ln, Aiken, SC 29801, USA
    ##   298-240 Magnolia St SE, Aiken, SC 29801, USA
    ##   Aiken, SC, USA
    ##   Vaucluse, SC 29801, USA
    ##   Aiken County, SC, USA
    ##   South Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.88819885,-76.30020142&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8528 W 49th St, Norfolk, VA 23508, USA
    ##   Rogers Hall Annex, 1055 W 49th St, Norfolk, VA 23529, USA
    ##   1049 W 49th St, Norfolk, VA 23508, USA
    ##   Highland Park, Norfolk, VA 23508, USA
    ##   Norfolk, VA 23508, USA
    ##   Norfolk, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.77749634,-106.490303&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1201 E Schuster Ave, El Paso, TX 79902, USA
    ##   1194 Rim Rd, El Paso, TX 79902, USA
    ##   Tom Lea Upper Park, 900 Rim Rd, El Paso, TX 79902, USA
    ##   Unnamed Road, El Paso, TX 79902, USA
    ##   West Central El Paso, El Paso, TX 79902, USA
    ##   El Paso, TX 79902, USA
    ##   El Paso, TX, USA
    ##   El Paso County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.34039307,-76.78820038&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6030 Larue St, Linglestown, PA 17112, USA
    ##   Koons Park, 630 Larue St, Linglestown, PA 17112, USA
    ##   1203 Balthaser St, Linglestown, PA 17112, USA
    ##   6104-6100 Nassau Rd, Linglestown, PA 17112, USA
    ##   Linglestown, PA 17112, USA
    ##   Lower Paxton Township, PA, USA
    ##   West Hanover Township, PA 17112, USA
    ##   Dauphin County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.96539307,-78.0358963&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   WB&S Old Railroad Grade, Southport, NC 28461, USA
    ##   7945 Long Beach Rd SE, Southport, NC 28461, USA
    ##   BLNG SPG LKS, NC 28461, USA
    ##   Smithville, NC, USA
    ##   Brunswick County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.8993988,-122.1143951&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3471 Sky Ln, Lafayette, CA 94549, USA
    ##   8 Sessions Rd, Lafayette, CA 94549, USA
    ##   1153 Sierra Vista Way, Lafayette, CA 94549, USA
    ##   3498 Sky Ln, Lafayette, CA 94549, USA
    ##   9-3 Sessions Rd, Lafayette, CA 94549, USA
    ##   Lafayette, CA, USA
    ##   Lafayette, CA 94549, USA
    ##   Contra Costa County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.94410706,-118.197998&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4161 Tweedy Blvd, South Gate, CA 90280, USA
    ##   9835 Otis St, South Gate, CA 90280, USA
    ##   Unnamed Road, South Gate, CA 90280, USA
    ##   South Gate, CA 90280, USA
    ##   South Gate, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.41430664,-3.701599121&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Plaza del Ángel, 8, 28012 Madrid, Spain
    ##   Plaza del Ángel, 7, 28012 Madrid, Spain
    ##   Plaza del Ángel, 9, 28012 Madrid, Spain
    ##   Plaza del Ángel, 28012 Madrid, Spain
    ##   Barrio de las Letras, Madrid, Spain
    ##   28012 Madrid, Spain
    ##   Centro, Madrid, Spain
    ##   Madrid, Spain
    ##   Municipality of Madrid, Madrid, Spain
    ##   Área Metropolitalitana y Corredor del Henares, Madrid, Spain
    ##   Community of Madrid, Madrid, Spain
    ##   Spain
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.50419617,-98.56970215&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7458 Louis Pasteur Dr, San Antonio, TX 78229, USA
    ##   5403 Fredericksburg Rd, San Antonio, TX 78229, USA
    ##   Unnamed Road, San Antonio, TX 78229, USA
    ##   San Antonio, TX 78229, USA
    ##   Northwest Side, San Antonio, TX, USA
    ##   San Antonio, TX, USA
    ##   Bexar County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.43240356,-79.92469788&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Davis Playground, 5680 Hobart St, Pittsburgh, PA 15217, USA
    ##   5700 Hobart St, Pittsburgh, PA 15217, USA
    ##   5702 Hobart St, Pittsburgh, PA 15217, USA
    ##   5673 Hobart St, Pittsburgh, PA 15217, USA
    ##   Squirrel Hill South, Pittsburgh, PA, USA
    ##   Pittsburgh, PA 15217, USA
    ##   Pittsburgh, PA, USA
    ##   Allegheny County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=21.45350647,-158.0193024&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Mililani Neighborhood Park, 95-245 Kaloapau St, Mililani, HI 96789, USA
    ##   95-245 Kaloapau St, Mililani, HI 96789, USA
    ##   95-203 Kahiku Pl, Mililani, HI 96789, USA
    ##   95 Kahiku Pl, Mililani, HI 96789, USA
    ##   Mililani, HI 96789, USA
    ##   O‘ahu, Hawaii, USA
    ##   Honolulu County, HI, USA
    ##   Hawaii, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.63000488,-122.2971954&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Seattle Japanese Garden, 1075 Lake Washington Blvd E, Seattle, WA 98112, USA
    ##   1195 Lake Washington Blvd E, Seattle, WA 98112, USA
    ##   1219-1201 Lake Washington Blvd E, Seattle, WA 98112, USA
    ##   Stevens, Seattle, WA, USA
    ##   Seattle, WA 98112, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.69839478,-87.70310211&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10713 S Spaulding Ave, Chicago, IL 60655, USA
    ##   10712 S Spaulding Ave, Chicago, IL 60655, USA
    ##   10719-10713 S Spaulding Ave, Chicago, IL 60655, USA
    ##   Mount Greenwood, Chicago, IL 60655, USA
    ##   MERRIONETT PK, IL 60655, USA
    ##   Chicago, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.55940247,-112.0902023&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Royal Palm Park, 8405 N 15th Ave, Phoenix, AZ 85021, USA
    ##   8405 N 15th St, Phoenix, AZ 85020, USA
    ##   8504 N 13th Ave, Phoenix, AZ 85021, USA
    ##   1413 W Butler Dr, Phoenix, AZ 85021, USA
    ##   8430 N 15th Ave, Phoenix, AZ 85021, USA
    ##   Phoenix, AZ 85021, USA
    ##   North Mountain Village, Phoenix, AZ, USA
    ##   Phoenix, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.51730347,-122.639801&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   804 SE 25th Ave, Portland, OR 97214, USA
    ##   SE 25th & Morrison, Portland, OR 97214, USA
    ##   810 SE 25th Ave, Portland, OR 97214, USA
    ##   2469 SE Morrison St, Portland, OR 97214, USA
    ##   898-800 SE 25th Ave, Portland, OR 97214, USA
    ##   Buckman Neighborhood, Portland, OR 97214, USA
    ##   Portland, OR 97214, USA
    ##   Southeast Portland, Portland, OR, USA
    ##   Portland, OR, USA
    ##   Multnomah County, OR, USA
    ##   Willamette Valley, Oregon, USA
    ##   Oregon, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.53399658,-83.52850342&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2943 W Maple Rd, Wixom, MI 48393, USA
    ##   2915 W Maple Rd, Wixom, MI 48393, USA
    ##   W Maple Rd, Wixom, MI 48393, USA
    ##   Wixom, MI, USA
    ##   Wixom, MI 48393, USA
    ##   Oakland County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.66419983,-80.17320251&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8532 Wendy Ln E, West Palm Beach, FL 33411, USA
    ##   8034 7th Pl S, West Palm Beach, FL 33411, USA
    ##   FL-91, West Palm Beach, FL 33413, USA
    ##   8001 7th Pl S, West Palm Beach, FL 33411, USA
    ##   West Palm Beach, FL 33411, USA
    ##   Palm Beach County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.45620728,-79.81629944&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   369 Whittier Dr, Pittsburgh, PA 15235, USA
    ##   760 Jefferson Rd, Pittsburgh, PA 15235, USA
    ##   Penn Hills Dog Park, 760 Jefferson Rd, Penn Hills, PA 15235, USA
    ##   368 Whittier Dr, Penn Hills, PA 15235, USA
    ##   Unnamed Road, Penn Hills, PA 15235, USA
    ##   Shadow Shuttle, Penn Hills, PA 15235, USA
    ##   Penn Hills, PA 15235, USA
    ##   Penn Hills Township, PA, USA
    ##   Penn Hills, PA, USA
    ##   Allegheny County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.72239685,-84.52050018&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4060 Danforth Rd SW, Atlanta, GA 30331, USA
    ##   1240 Kimberly Rd SW, Atlanta, GA 30331, USA
    ##   1235 Kimberly Rd SW, Atlanta, GA 30331, USA
    ##   1335 Kimberly Rd SW, Atlanta, GA 30331, USA
    ##   Kimberly Rd @ Fairly Way, Atlanta, GA 30331, USA
    ##   Kimberly Rd SW, Atlanta, GA 30331, USA
    ##   Atlanta, GA 30331, USA
    ##   South Fulton, GA, USA
    ##   Fulton County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-22.71589661,-47.77340698&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Piracicaba - SP, Brazil
    ##   Piracicaba - State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.39050293,-81.33740234&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   579 E 1st St, Uhrichsville, OH 44683, USA
    ##   586 E 1st St, Uhrichsville, OH 44683, USA
    ##   590 E 1st St, Uhrichsville, OH 44683, USA
    ##   613-579 E 1st St, Uhrichsville, OH 44683, USA
    ##   Uhrichsville, OH 44683, USA
    ##   Mill Township, OH, USA
    ##   Tuscarawas County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.24229431,-97.76719666&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   South Austin Neighborhood Park, 1100 Cumberland Rd, Austin, TX 78704, USA
    ##   1113 Fieldcrest Dr, Austin, TX 78704, USA
    ##   2499 Stone Crest Dr, Austin, TX 78704, USA
    ##   S Austin Tennis Center Pedestrian Walkway, Austin, TX 78704, USA
    ##   Austin, TX 78704, USA
    ##   South Austin, Austin, TX, USA
    ##   Austin, TX, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.63789368,-70.51889801&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1228 Long Plains Rd, Buxton, ME 04093, USA
    ##   1221 Long Plains Rd, Buxton, ME 04093, USA
    ##   1223 Long Plains Rd, Buxton, ME 04093, USA
    ##   1276-1242 Long Plains Rd, Buxton, ME 04093, USA
    ##   Buxton, ME 04093, USA
    ##   Buxton, ME, USA
    ##   York County, ME, USA
    ##   Maine, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.93539429,-93.16940308&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   223 Macalester St, St Paul, MN 55105, USA
    ##   St Clair Ave & Macalester St, St Paul, MN 55105, USA
    ##   1600 Grand Ave, St Paul, MN 55105, USA
    ##   Unnamed Road, St Paul, MN 55105, USA
    ##   Macalester - Groveland, St Paul, MN, USA
    ##   St Paul, MN 55105, USA
    ##   St Paul, MN, USA
    ##   Ramsey County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.72729492,-73.66960144&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   107 Sunset Terrace, Troy, NY 12180, USA
    ##   109 Sunset Terrace, Troy, NY 12180, USA
    ##   Sunset Terrace, Troy, NY 12180, USA
    ##   Troy, NY, USA
    ##   Troy, NY 12180, USA
    ##   Rensselaer County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.70329285,-87.82980347&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8659 W 103rd St, Palos Hills, IL 60465, USA
    ##   8455 W 103rd St, Palos Hills, IL 60465, USA
    ##   8501 W 103rd St, Palos Hills, IL 60465, USA
    ##   103rd St, Palos Hills, IL 60465, USA
    ##   Palos Hills, IL 60465, USA
    ##   Palos Township, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   3154 E Skyline Dr, San Tan Valley, AZ 85140, USA
    ##   San Tan Valley, AZ, USA
    ##   Queen Creek, AZ 85140, USA
    ##   Pinal County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.00349426,-117.0695953&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   15940 Bernardo Heights Pkwy, San Diego, CA 92128, USA
    ##   16066 Bernardo Heights Pkwy, San Diego, CA 92128, USA
    ##   Bernardo Heights Pkwy, San Diego, CA 92128, USA
    ##   San Diego, CA 92128, USA
    ##   Rancho Bernardo, San Diego, CA, USA
    ##   San Diego, CA, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   3007 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   3702 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   S Ridge Trail, Yorba Linda, CA 92886, USA
    ##   Yorba Linda, CA 92886, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.25190735,-81.76360321&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2590 Tiburon Dr, Naples, FL 34109, USA
    ##   Tiburon Blvd E, Naples, FL 34109, USA
    ##   2738 Tiburon Blvd E, Naples, FL 34109, USA
    ##   Naples, FL 34109, USA
    ##   North Naples, FL, USA
    ##   Collier County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.06230164,-86.0585022&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   88 Mill Farm Rd, Noblesville, IN 46062, USA
    ##   66 Mill Farm Rd, Noblesville, IN 46062, USA
    ##   75 N Mill Creek Rd, Noblesville, IN 46062, USA
    ##   190-92 N Mill Creek Rd, Noblesville, IN 46062, USA
    ##   Westfield, IN 46062, USA
    ##   Noblesville Township, IN, USA
    ##   Hamilton County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   530 Cliffs Dr, Ypsilanti, MI 48198, USA
    ##   5149-5101 Applewood Dr, Ypsilanti, MI 48197, USA
    ##   Ypsilanti Charter Twp, MI, USA
    ##   Ypsilanti, MI 48197, USA
    ##   Washtenaw County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=52.53529358,13.42449951&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Marienburger Str. 40A, 10405 Berlin, Germany
    ##   Marienburger Str. 34, 10405 Berlin, Germany
    ##   Marienburger Str. 5-7, 10405 Berlin, Germany
    ##   Winsviertel, Berlin, Germany
    ##   10405 Berlin, Germany
    ##   Prenzlauer Berg, Berlin, Germany
    ##   Pankow, Berlin, Germany
    ##   Berlin, Germany
    ##   Germany
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.22569275,-95.49240112&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Deep Gully Trail South, Conroe, TX 77384, USA
    ##   W G Jones State Forest, 1328 Farm to Market Rd 1488, Conroe, TX 77384, USA
    ##   Conroe, TX 77384, USA
    ##   Conroe, TX, USA
    ##   Montgomery County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.14480591,-118.3666992&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4057 Riverton Ave, Studio City, CA 91602, USA
    ##   10820 Acama St, Studio City, CA 91602, USA
    ##   4089 Riverton Ave, Studio City, CA 91602, USA
    ##   4159-4101 Riverton Ave, Studio City, CA 91602, USA
    ##   North Hollywood, CA 91602, USA
    ##   Studio City, Los Angeles, CA, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.49859619,-81.53530121&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Park Among the Lakes, E 3rd Ave, Windermere, FL 34786, USA
    ##   219 Main St, Windermere, FL 34786, USA
    ##   211 Main St, Windermere, FL 34786, USA
    ##   146 E 3rd Ave, Windermere, FL 34786, USA
    ##   505-301 Oakdale St, Windermere, FL 34786, USA
    ##   Windermere, FL 34786, USA
    ##   Orange County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.87820435,-72.95249939&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Middle Island by field stand, 197 Middle Country Rd, Middle Island, NY 11953, USA
    ##   197 Middle Country Rd, Middle Island, NY 11953, USA
    ##   Unnamed Road, Middle Island, NY 11953, USA
    ##   Middle Island, NY 11953, USA
    ##   Brookhaven, NY, USA
    ##   Long Island, New York, USA
    ##   Suffolk County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.66769409,-121.6595993&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   104 Lang St, Salinas, CA 93901, USA
    ##   109 Lang St, Salinas, CA 93901, USA
    ##   726 S Main St, Salinas, CA 93901, USA
    ##   699-561 Capitol St, Salinas, CA 93901, USA
    ##   Salinas, CA 93901, USA
    ##   Salinas, CA, USA
    ##   Monterey County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.98980713,-76.79039764&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   12213 Quick Fox Ln, Bowie, MD 20720, USA
    ##   7206 Quisinberry Way, Bowie, MD 20720, USA
    ##   7200 Quisinberry Way, Bowie, MD 20720, USA
    ##   Quisinberry Way, Bowie, MD 20720, USA
    ##   Bowie, MD 20720, USA
    ##   Bowie, MD, USA
    ##   Prince George's County, MD, USA
    ##   Maryland, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.60920715,-122.3314056&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Seneca Plaza, 900 Seneca St, Seattle, WA 98101, USA
    ##   1200 6th Ave, Seattle, WA 98101, USA
    ##   Seneca St & 6th Ave, Seattle, WA 98101, USA
    ##   I-5, Seattle, WA 98101, USA
    ##   Central Business District, Seattle, WA, USA
    ##   Seattle, WA 98101, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.80589294,-117.3466034&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   20177 Piedras Rd, Perris, CA 92570, USA
    ##   21529-20733 Piedras Rd, Perris, CA 92570, USA
    ##   LAKE MATHEWS, CA 92570, USA
    ##   Riverside County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.80189514,-84.38610077&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1710 Barnesdale Way NE, Atlanta, GA 30309, USA
    ##   1704 Nottingham Way NE, Atlanta, GA 30309, USA
    ##   Buford Spring Connector, Atlanta, GA 30309, USA
    ##   1709 Barnesdale Way NE, Atlanta, GA 30309, USA
    ##   Sherwood Forest, Atlanta, GA 30309, USA
    ##   Atlanta, GA 30309, USA
    ##   Midtown, Atlanta, GA, USA
    ##   Atlanta, GA, USA
    ##   Fulton County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.31059265,-80.14289856&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2010 Islewood D, Deerfield Beach, FL 33442, USA
    ##   Century Village, Deerfield Beach, FL 33442, USA
    ##   Deerfield Beach, FL 33442, USA
    ##   Deerfield Beach, FL, USA
    ##   Broward County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.06829834,-123.0763016&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2295 Oakmont Way, Eugene, OR 97401, USA
    ##   2260 Bedford Way, Eugene, OR 97401, USA
    ##   2306 Oakmont Way, Eugene, OR 97401, USA
    ##   2200-2302 Oakmont Way, Eugene, OR 97401, USA
    ##   Cal Young, Eugene, OR 97401, USA
    ##   Eugene, OR 97401, USA
    ##   Eugene, OR, USA
    ##   Willamette Valley, Oregon, USA
    ##   Lane County, OR, USA
    ##   Oregon, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.04469299,-118.4487&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   11340 Iowa Ave, Los Angeles, CA 90025, USA
    ##   1674 Corinth Ave, Los Angeles, CA 90025, USA
    ##   11355 Iowa Ave, Los Angeles, CA 90025, USA
    ##   11338 Santa Monica Blvd, Los Angeles, CA 90025, USA
    ##   1798-1700 Corinth Ave, Los Angeles, CA 90025, USA
    ##   West Los Angeles, CA 90025, USA
    ##   Sawtelle, Los Angeles, CA, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.51089478,-84.97940063&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1024 Maridele Dr, Columbus, GA 31904, USA
    ##   4600 River Rd, Columbus, GA 31904, USA
    ##   4900 Morris Ave, Columbus, GA 31904, USA
    ##   4997-4901 Morris Ave, Columbus, GA 31904, USA
    ##   Columbus, GA 31904, USA
    ##   Muscogee County, Columbus, GA, USA
    ##   Columbus, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.68409729,-81.28119659&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   560 Dunmar Cir, Winter Springs, FL 32708, USA
    ##   Unnamed Road, Winter Springs, FL 32708, USA
    ##   Winter Springs, FL, USA
    ##   Winter Springs, FL 32708, USA
    ##   Seminole County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=27.67759705,-97.36509705&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2801 Airline Rd, Corpus Christi, TX 78414, USA
    ##   6610 Saratoga Blvd, Corpus Christi, TX 78414, USA
    ##   2804 Airline Rd, Corpus Christi, TX 78414, USA
    ##   2647-2799 Airline Rd, Corpus Christi, TX 78414, USA
    ##   Corpus Christi, TX 78414, USA
    ##   South Side, Corpus Christi, TX, USA
    ##   Corpus Christi, TX, USA
    ##   Nueces County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.21530151,-73.12329865&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   178 Elizabeth Terrace, Stratford, CT 06614, USA
    ##   100 Elmhurst Ave, Stratford, CT 06614, USA
    ##   111 Elmhurst Ave, Stratford, CT 06614, USA
    ##   151-199 Elizabeth Terrace, Stratford, CT 06614, USA
    ##   Stratford, CT 06614, USA
    ##   Stratford, CT, USA
    ##   Fairfield County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.8453064,-74.70189667&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1 Laurel Dr, Flanders, NJ 07836, USA
    ##   2 Laurel Dr, Flanders, NJ 07836, USA
    ##   20 Laurel Dr, Flanders, NJ 07836, USA
    ##   US-206, Flanders, NJ 07836, USA
    ##   Flanders, Mt Olive Township, NJ 07836, USA
    ##   Flanders, NJ 07836, USA
    ##   Mt Olive Township, NJ, USA
    ##   Morris County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.83360291,-84.37969971&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2890 N Fulton Dr NE, Atlanta, GA 30305, USA
    ##   Unnamed Road, Atlanta, GA 30305, USA
    ##   Garden Hills, Atlanta, GA 30305, USA
    ##   Atlanta, GA 30305, USA
    ##   Atlanta, GA, USA
    ##   Fulton County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.41549683,-80.61430359&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   631 Concord Pkwy N, Concord, NC 28027, USA
    ##   2300 Eva Dr NW, Concord, NC 28027, USA
    ##   605 Concord Pkwy N, Concord, NC 28027, USA
    ##   Concord Pkwy N, Concord, NC 28027, USA
    ##   2, Poplar Tent, NC, USA
    ##   Concord, NC, USA
    ##   Concord, NC 28027, USA
    ##   Cabarrus County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.44850159,-82.20110321&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   200 Newmantown Rd, Grovetown, GA 30813, USA
    ##   208-1/2 Newmantown Rd, Grovetown, GA 30813, USA
    ##   104 Old Berzelia Rd, Grovetown, GA 30813, USA
    ##   Spring St, Grovetown, GA 30813, USA
    ##   Grovetown, GA 30813, USA
    ##   Columbia County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.71170044,-96.9992981&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2328 Acosta St, Grand Prairie, TX 75051, USA
    ##   2399-2341 Acosta St, Grand Prairie, TX 75051, USA
    ##   Grand Prairie, TX 75051, USA
    ##   Grand Prairie, TX, USA
    ##   Dallas County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.80880737,-73.91950226&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Saw Mill Playground, 488 E 139th St, The Bronx, NY 10454, USA
    ##   468 E 140th St, The Bronx, NY 10454, USA
    ##   482F E 139th St, The Bronx, NY 10454, USA
    ##   484 E 139th St, The Bronx, NY 10454, USA
    ##   Mott Haven, The Bronx, NY, USA
    ##   The Bronx, NY 10454, USA
    ##   The Bronx, NY, USA
    ##   Bronx County, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-23.1309967,-46.58900452&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   R. Edmundo Zanoni, 196 - Jardim das Cerejeiras, Atibaia - SP, 12951-030, Brazil
    ##   R. Edmundo Zanoni, 194 - Jardim das Cerejeiras, Atibaia - SP, 12951-030, Brazil
    ##   Cerejeiras III Glebas, Atibaia - SP, Brazil
    ##   R. José de Campos - Casas Populares, Atibaia - SP, 12951-088, Brazil
    ##   Atibaia - State of São Paulo, Brazil
    ##   Atibaia, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.83790588,-87.82129669&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   318 Northwood Rd, Riverside, IL 60546, USA
    ##   323 Northwood Rd, Riverside, IL 60546, USA
    ##   316 Northwood Rd, Riverside, IL 60546, USA
    ##   368-322 Northwood Rd, Riverside, IL 60546, USA
    ##   Riverside, IL 60546, USA
    ##   Riverside Township, IL, USA
    ##   North Riverside, IL 60546, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.67329407,-122.3426056&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6253 West Green Lake Way N, Seattle, WA 98115, USA
    ##   Green Lake Trail, Seattle, WA 98115, USA
    ##   Green Lake, Seattle, WA, USA
    ##   Seattle, WA 98115, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.23449707,-85.72360229&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Louisville, KY 40204, USA
    ##   Tyler Park, Louisville, KY, USA
    ##   Louisville, KY 40204, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.38589478,-122.0881958&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   McKelvey Park, 1101-1197 Park Dr, Mountain View, CA 94040, USA
    ##   1000 Miramonte Ave, Mountain View, CA 94040, USA
    ##   Miramonte Ave, Mountain View, CA 94040, USA
    ##   Mountain View, CA 94040, USA
    ##   Mountain View, CA, USA
    ##   San Francisco Peninsula, California, USA
    ##   Santa Clara County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.9683075,-95.26950073&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Ludlam Park, 2800 W 9th St, Lawrence, KS 66049, USA
    ##   2800 W 9th St, Lawrence, KS 66049, USA
    ##   818 Schwarz Rd, Lawrence, KS 66049, USA
    ##   2808 W 9th St, Lawrence, KS 66049, USA
    ##   998-900 Schwarz Rd, Lawrence, KS 66049, USA
    ##   Sunset Hills, Lawrence, KS, USA
    ##   Lawrence, KS, USA
    ##   Lawrence, KS 66049, USA
    ##   Douglas County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.7960968,-73.95130157&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5 Av/E 108 St, New York, NY 10029, USA
    ##   Unnamed Road, New York, NY 10029, USA
    ##   New York, NY 10029, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.54110718,-122.5605011&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2505 NE 102nd Ave, Portland, OR 97220, USA
    ##   Vietnam Veterans Memorial Hwy, Portland, OR 97220, USA
    ##   Madison South, Portland, OR, USA
    ##   Portland, OR 97220, USA
    ##   Portland, OR, USA
    ##   Multnomah County, OR, USA
    ##   Oregon, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.90730286,-105.0156021&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2400 Country Club Loop, Westminster, CO 80234, USA
    ##   2410 Country Club Loop, Westminster, CO 80234, USA
    ##   2361 Country Club Loop, Westminster, CO 80234, USA
    ##   2341 Country Club Loop, Westminster, CO 80234, USA
    ##   North Central Westminster, Westminster, CO, USA
    ##   Denver, CO 80234, USA
    ##   Westminster, CO, USA
    ##   Adams County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.55180359,-111.8918991&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7079 E Panorama Dr, Idaho Falls, ID 83401, USA
    ##   6833 E Panorama Dr, Idaho Falls, ID 83401, USA
    ##   7060 E Panorama Dr, Idaho Falls, ID 83401, USA
    ##   6862-7048 E Panorama Dr, Idaho Falls, ID 83401, USA
    ##   Idaho Falls, ID 83401, USA
    ##   Bonneville County, ID, USA
    ##   Idaho, USA
    ##   Rocky Mountains
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-33.87759399,151.0846863&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   20 Florence St, Strathfield NSW 2135, Australia
    ##   15 Florence St, Strathfield NSW 2135, Australia
    ##   2-20 Florence St, Strathfield NSW 2135, Australia
    ##   Strathfield NSW 2135, Australia
    ##   Strathfield, NSW, Australia
    ##   Sydney NSW, Australia
    ##   New South Wales, Australia
    ##   Australia
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.45280457,-110.7393036&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Jackson, WY 83001, USA
    ##   Jackson, WY 83001, USA
    ##   Teton County, WY, USA
    ##   Wyoming, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.71780396,-78.84279633&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1005 Marco Dr, Apex, NC 27502, USA
    ##   1164 E Williams St, Apex, NC 27502, USA
    ##   Apex Peakway, Apex, NC 27502, USA
    ##   Apex, NC 27502, USA
    ##   White Oak, NC, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.21299744,-86.30110168&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   504 Hill St, Lebanon, TN 37087, USA
    ##   505 Hill St, Lebanon, TN 37087, USA
    ##   111-131 Hammond Ave, Lebanon, TN 37087, USA
    ##   Lebanon, TN, USA
    ##   Lebanon, TN 37087, USA
    ##   Wilson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.0717926,-117.6972961&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10055 Monte Vista Ave, Montclair, CA 91763, USA
    ##   4900 Orchard St, Montclair, CA 91763, USA
    ##   4937 Denver St, Montclair, CA 91763, USA
    ##   9982-10026 Monte Vista Ave, Montclair, CA 91763, USA
    ##   Montclair, CA 91763, USA
    ##   Montclair, CA, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.7467041,-122.3685989&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   148 Moss Rd, Shoreline, WA 98177, USA
    ##   146 Moss Rd, Shoreline, WA 98177, USA
    ##   Fredrick PI NW, Shoreline, WA 98177, USA
    ##   143 Moss Rd, Shoreline, WA 98177, USA
    ##   The Highlands, Shoreline, WA 98177, USA
    ##   Seattle, WA 98177, USA
    ##   Shoreline, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.07739258,-71.04460144&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   332 West St, Brockton, MA 02301, USA
    ##   West Street and Neubert Street, Brockton, MA 02301, USA
    ##   53 Morse Ave, Brockton, MA 02301, USA
    ##   345 West St, Brockton, MA 02301, USA
    ##   85 Morse Ave, Brockton, MA 02301, USA
    ##   315-325 West St, Brockton, MA 02301, USA
    ##   Brockton, MA 02301, USA
    ##   Brockton, MA, USA
    ##   Plymouth County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.56939697,-101.7193985&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Johnson City, KS 67855, USA
    ##   Stanton, KS, USA
    ##   Johnson City, KS 67855, USA
    ##   Stanton County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.62260437,-111.7777023&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4193 Canyon Estate Dr, Cottonwood Heights, UT 84121, USA
    ##   4141 Canyon Estate Dr, Cottonwood Heights, UT 84121, USA
    ##   Canyon Estate Dr, Cottonwood Heights, UT 84121, USA
    ##   Cottonwood Heights, UT, USA
    ##   Salt Lake City, UT 84121, USA
    ##   Salt Lake County, UT, USA
    ##   Utah, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.34109497,-90.32289886&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   517 E Leake St, Clinton, MS 39056, USA
    ##   513 Dunton Rd, Clinton, MS 39056, USA
    ##   509 E Leake St, Clinton, MS 39056, USA
    ##   420-598 Dunton Rd, Clinton, MS 39056, USA
    ##   Clinton, MS, USA
    ##   Clinton, MS 39056, USA
    ##   Hinds County, MS, USA
    ##   Mississippi, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   3007 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   3702 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   S Ridge Trail, Yorba Linda, CA 92886, USA
    ##   Yorba Linda, CA 92886, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.54229736,-89.95880127&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   220 Lake Christine Dr, Belleville, IL 62221, USA
    ##   300 Lake Christine Dr, Belleville, IL 62221, USA
    ##   278 Lake Christine Dr, Belleville, IL 62221, USA
    ##   200-298 Sunnyslope Dr, Belleville, IL 62221, USA
    ##   St Clair Township, IL, USA
    ##   Swansea, IL 62221, USA
    ##   St Clair County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   17742 NW Pioneer Rd, Beaverton, OR 97006, USA
    ##   17664 NW Shady Fir Loop, Beaverton, OR 97006, USA
    ##   Triple Creek, Beaverton, OR 97006, USA
    ##   Hillsboro, OR 97006, USA
    ##   Beaverton, OR, USA
    ##   Washington County, OR, USA
    ##   Willamette Valley, Oregon, USA
    ##   Oregon, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.90179443,-72.88809967&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   432 Randall Rd, Ridge, NY 11961, USA
    ##   442 Randall Rd, Ridge, NY 11961, USA
    ##   427 Randall Rd, Ridge, NY 11961, USA
    ##   9-1 Redbrook Ln, Ridge, NY 11961, USA
    ##   Ridge, NY, USA
    ##   Ridge, NY 11961, USA
    ##   Brookhaven, NY, USA
    ##   Long Island, New York, USA
    ##   Suffolk County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.92520142,-74.17810059&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5 N 4th St, Paterson, NJ 07522, USA
    ##   3 N 4th St, Paterson, NJ 07522, USA
    ##   91-95 Cliff St, Paterson, NJ 07522, USA
    ##   4 N 4th St, Paterson, NJ 07522, USA
    ##   99-1 Arlington St, Paterson, NJ 07522, USA
    ##   Paterson, NJ 07522, USA
    ##   Paterson, NJ, USA
    ##   Passaic County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.38330078,-79.69999695&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   45 Perry St, Barrie, ON L4N 2G3, Canada
    ##   2-8 Frances St S, Barrie, ON L4N 1Y9, Canada
    ##   Barrie, ON L4N 2G2, Canada
    ##   Barrie, ON L4N, Canada
    ##   Barrie, ON, Canada
    ##   Simcoe County, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   1201 Valerie Ave NE, Massillon, OH 44646, USA
    ##   2100 Carlyle St NW, Massillon, OH 44646, USA
    ##   1147 Valerie Ave NE, Massillon, OH 44646, USA
    ##   1400-1448 Valerie Ave NE, Massillon, OH 44646, USA
    ##   Massillon, OH, USA
    ##   Massillon, OH 44646, USA
    ##   Stark County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.77459717,-88.43759918&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   233 3rd St, Fond du Lac, WI 54935, USA
    ##   242 E 2nd St, Fond du Lac, WI 54935, USA
    ##   235 3rd St, Fond du Lac, WI 54935, USA
    ##   Fond du Lac, WI, USA
    ##   Taycheedah, WI 54935, USA
    ##   Fond Du Lac County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.07359314,-97.47270203&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1400 N Loop 121, Belton, TX 76513, USA
    ##   542 N Loop 121, Belton, TX 76513, USA
    ##   603-577 N Loop 121, Belton, TX 76513, USA
    ##   Belton, TX, USA
    ##   MORGANS POINT, TX 76513, USA
    ##   Bell County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.04139709,-84.50530243&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3805 Maple Ct, Marietta, GA 30066, USA
    ##   3785 Maple Ct, Marietta, GA 30066, USA
    ##   3722 Willow Wind Dr, Marietta, GA 30066, USA
    ##   1620 Willow Wind Dr, Marietta, GA 30066, USA
    ##   Marietta, GA 30066, USA
    ##   Cobb County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.76010132,-93.27480316&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   13405 1st Ave S, Burnsville, MN 55337, USA
    ##   16 Knoll Ln, Burnsville, MN 55337, USA
    ##   115 E 135th St, Burnsville, MN 55337, USA
    ##   13499-13405 1st Ave S, Burnsville, MN 55337, USA
    ##   Burnsville, MN 55337, USA
    ##   Burnsville, MN, USA
    ##   Dakota County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Margaret Hunt Hill Bridge, Margaret Hunt Hill Bridge, Dallas, TX 75207, USA
    ##   Trinity Skyline Trail, Dallas, TX 75207, USA
    ##   1001 Continental St Via, Dallas, TX 75212, USA
    ##   Dallas, TX 75207, USA
    ##   Dallas, TX, USA
    ##   Dallas County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.45939636,-87.20749664&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4123 Menendez Dr, Pensacola, FL 32503, USA
    ##   1211-1299 Driftwood Dr, Pensacola, FL 32503, USA
    ##   Southeast Pensacola, Pensacola, FL, USA
    ##   Pensacola, FL 32503, USA
    ##   Pensacola, FL, USA
    ##   Escambia County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.54580688,-88.10189819&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2801 County RK, Green Bay, WI 54303, USA
    ##   1810 Riverdale Dr, Hobart, WI 54313, USA
    ##   Riverdale Dr, Hobart, WI 54313, USA
    ##   Howard, WI, USA
    ##   Green Bay, WI 54313, USA
    ##   Brown County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Via Statilia Park, Via Statilia, 00185 Roma RM, Italy
    ##   Via S. Croce In Gerusalemme/Statilia, 00185 Roma RM, Italy
    ##   Via Statilia, 21, 00185 Roma RM, Italy
    ##   Via di S. Croce in Gerusalemme, 38, 00185 Roma RM, Italy
    ##   Via Statilia, 00185 Roma RM, Italy
    ##   Esquilino, Rome, Metropolitan City of Rome, Italy
    ##   00185 Rome, Metropolitan City of Rome, Italy
    ##   Municipio I, Rome, Metropolitan City of Rome, Italy
    ##   Rome, Metropolitan City of Rome, Italy
    ##   Metropolitan City of Rome, Italy
    ##   Lazio, Italy
    ##   Italy
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.30299377,-76.88619995&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   North Hall, Gate 5, Harrisburg, PA 17110, USA
    ##   N Hall Dr, Harrisburg, PA 17110, USA
    ##   1 HACC Dr, Harrisburg, PA 17110, USA
    ##   Harrisburg, PA, USA
    ##   Harrisburg, PA 17110, USA
    ##   Dauphin County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1/A, Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka 560001, India
    ##   Unnamed Road, Ambedkar Veedhi, Bengaluru, Karnataka 560001, India
    ##   Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka, India
    ##   Bengaluru, Karnataka 560001, India
    ##   Bengaluru, Karnataka, India
    ##   Bangalore Urban, Karnataka, India
    ##   Karnataka, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=48.01319885,-122.0679016&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1706 123rd Dr NE, Lake Stevens, WA 98258, USA
    ##   12301 17th Pl NE, Lake Stevens, WA 98258, USA
    ##   12046-11910 N Lakeshore Dr, Lake Stevens, WA 98258, USA
    ##   West Lake Stevens, WA, USA
    ##   Lake Stevens, WA 98258, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.70939636,-98.02980042&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   105 S Sanborn Blvd, Mitchell, SD 57301, USA
    ##   403 W 1st Ave, Mitchell, SD 57301, USA
    ##   S Sanborn Blvd, Mitchell, SD 57301, USA
    ##   Mitchell, SD 57301, USA
    ##   Davison County, SD, USA
    ##   South Dakota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.45370483,-73.1772995&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Kennedy Drive at South Burlington High School, South Burlington, VT 05403, USA
    ##   2 Kennedy Dr, South Burlington, VT 05403, USA
    ##   20 Kennedy Dr, South Burlington, VT 05403, USA
    ##   Kennedy Dr, South Burlington, VT 05403, USA
    ##   South Burlington, VT 05403, USA
    ##   South Burlington, VT, USA
    ##   Chittenden County, VT, USA
    ##   Vermont, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=17.38409424,78.45639038&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   13, Sitaram Bagh - Dhoolpet Rd, Aziz Bagh, Sitaram Bagh, Hyderabad, Telangana 500028, India
    ##   Sitaram Bagh - Dhoolpet Rd, Aziz Bagh, Sitaram Bagh, Hyderabad, Telangana 500028, India
    ##   Sitaram Bagh, Hyderabad, Telangana, India
    ##   Hyderabad, Telangana 500006, India
    ##   Hyderabad, Telangana, India
    ##   Telangana, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.20030212,-118.4044952&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7133 Whitsett Ave, North Hollywood, CA 91605, USA
    ##   7152 Whitsett Ave, North Hollywood, CA 91605, USA
    ##   7100-7130 Whitsett Ave, North Hollywood, CA 91605, USA
    ##   Valley Glen, Los Angeles, CA, USA
    ##   North Hollywood, CA 91605, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.94760132,-73.86239624&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   29-99 Barton Rd, Yonkers, NY 10701, USA
    ##   133 Longspur Rd, Yonkers, NY 10701, USA
    ##   77 Barton Rd, Yonkers, NY 10701, USA
    ##   99-1 Victoria Ln, Yonkers, NY 10701, USA
    ##   Bryn Mawr, Yonkers, NY 10701, USA
    ##   Yonkers, NY 10701, USA
    ##   Yonkers, NY, USA
    ##   Westchester County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=25.72590637,-80.4036026&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4413 SW 129th Ave, Miami, FL 33175, USA
    ##   4415 SW 129th Ave, Miami, FL 33175, USA
    ##   SW 44th Terrace, Miami, FL 33175, USA
    ##   Miami, FL 33175, USA
    ##   Kendale Lakes, FL, USA
    ##   Miami-Dade County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.1723938,-115.0677032&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Las Vegas Wash Trail, Las Vegas, NV 89110, USA
    ##   539 Bayberry Dr, Las Vegas, NV 89110, USA
    ##   Las Vegas, NV 89110, USA
    ##   Las Vegas, NV, USA
    ##   Clark County, NV, USA
    ##   Nevada, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.69630432,-87.6576004&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10839 S Glenroy Ave, Chicago, IL 60643, USA
    ##   1358 W 109th St, Chicago, IL 60643, USA
    ##   8266 S Bishop St, Chicago, IL 60643, USA
    ##   1399-1393 S Bishop St, Chicago, IL 60643, USA
    ##   Morgan Park, Chicago, IL, USA
    ##   Calumet Park, IL 60643, USA
    ##   Chicago, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.210495,-85.6269989&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3502 Hillcreek Rd, Louisville, KY 40220, USA
    ##   3508 Hillcreek Rd, Louisville, KY 40220, USA
    ##   Breckenridge @ Hillcreek, Louisville, KY 40220, USA
    ##   3120 Breckenridge Ln, Louisville, KY 40220, USA
    ##   3116 Breckenridge Ln, Louisville, KY 40220, USA
    ##   Breckenridge Ln, Louisville, KY 40220, USA
    ##   Hikes Point, Louisville, KY 40220, USA
    ##   St Regis Park, KY 40220, USA
    ##   Louisville, KY, USA
    ##   Jefferson County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.3572998,-90.64980316&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4 Rustic Spring Ct, Cedar Hill, MO 63016, USA
    ##   8 Cedar Hill Estates, Cedar Hill, MO 63016, USA
    ##   6306-6292 Twin Springs Blvd, Cedar Hill, MO 63016, USA
    ##   Cedar Hill, MO 63016, USA
    ##   Meramec, MO, USA
    ##   Jefferson County, MO, USA
    ##   Missouri, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1020 Duluth St, St Paul, MN 55106, USA
    ##   1034 Duluth St, St Paul, MN 55106, USA
    ##   1118-1200 Jenks Ave E, St Paul, MN 55106, USA
    ##   Payne - Phalen, St Paul, MN, USA
    ##   St Paul, MN 55106, USA
    ##   St Paul, MN, USA
    ##   Ramsey County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Columbus Park, Mulberry Street &, Baxter St, New York, NY 10013, United States
    ##   95 Bayard St, New York, NY 10013, USA
    ##   78 Baxter St, New York, NY 10013, USA
    ##   35 Baxter St, New York, NY 10013, USA
    ##   New York, NY 10013, USA
    ##   Lower Manhattan, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.39079285,-111.9184036&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Hollis Park, 3421 S Kenneth Pl, Tempe, AZ 85282, USA
    ##   3466 S Kenneth Pl, Tempe, AZ 85282, USA
    ##   1201-1299 E Laguna Dr, Tempe, AZ 85282, USA
    ##   Tempe, AZ 85282, USA
    ##   South Tempe, Tempe, AZ, USA
    ##   Tempe, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.06599426,-86.96589661&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   708 Rock Harbour Ct, Nashville, TN 37221, USA
    ##   7713 Scenic River Ln, Nashville, TN 37221, USA
    ##   7567 Rolling River Pkwy, Nashville, TN 37221, USA
    ##   731 Rock Harbour Ct, Nashville, TN 37221, USA
    ##   6900-6998 River Ridge Dr, Nashville, TN 37221, USA
    ##   Bellevue, TN 37221, USA
    ##   Bellevue, Nashville, TN, USA
    ##   Nashville, TN, USA
    ##   Davidson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.60079956,-122.3247986&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   601 S Washington St, Seattle, WA 98104, USA
    ##   630 S Washington St, Seattle, WA 98104, USA
    ##   648 S Washington St, Seattle, WA 98104, USA
    ##   601-649 S Washington St, Seattle, WA 98104, USA
    ##   Seattle Chinatown-International District, Seattle, WA, USA
    ##   Seattle, WA 98104, USA
    ##   Downtown Seattle, Seattle, WA, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.45669556,-71.37470245&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1405 Main St, Concord, MA 01742, USA
    ##   Concord, MA, USA
    ##   Concord, MA 01742, USA
    ##   Middlesex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.70150757,-117.7528&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Lamplighter Park, 39 Enchanted, Irvine, CA 92620, USA
    ##   42 Enchanted, Irvine, CA 92620, USA
    ##   160 Vintage, Irvine, CA 92620, USA
    ##   Vintage, Irvine, CA 92620, USA
    ##   Woodbury, Irvine, CA 92620, USA
    ##   Irvine, CA 92620, USA
    ##   Irvine, CA, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.98269653,-70.94719696&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Exeter, NH 03833, USA
    ##   Exeter, NH 03833, USA
    ##   Kensington, NH 03833, USA
    ##   Rockingham County, NH, USA
    ##   New Hampshire, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.61810303,-83.78900146&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   445 GA-49, Byron, GA 31008, USA
    ##   GA-540, Byron, GA 31008, USA
    ##   245 GA-49, Byron, GA 31008, USA
    ##   Powersville, GA 31008, USA
    ##   Peach County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.94020081,-93.21880341&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3435 36th Ave S, Minneapolis, MN 55406, USA
    ##   3726 E 35th St, Minneapolis, MN 55406, USA
    ##   3798-3750 E 35th St, Minneapolis, MN 55406, USA
    ##   Howe, Minneapolis, MN 55406, USA
    ##   Minneapolis, MN 55406, USA
    ##   Minneapolis, MN, USA
    ##   Hennepin County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.96479797,-83.12599945&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4533 Fisher Rd, Columbus, OH 43291, USA
    ##   Unnamed Road, Columbus, OH 43291, USA
    ##   Columbus, OH 43291, USA
    ##   Columbus, OH, USA
    ##   Franklin County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.30459595,-118.6844025&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Marr Ranch Rd, Simi Valley, CA 93063, USA
    ##   Santa Susana, CA 93063, USA
    ##   Ventura County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.69520569,-122.6540985&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   10115 NE Hwy 99, Vancouver, WA 98686, USA
    ##   10127 NE Hwy 99, Vancouver, WA 98686, USA
    ##   NE Hwy 99, Vancouver, WA 98686, USA
    ##   Salmon Creek, WA, USA
    ##   Pleasant Valley, Battle Ground, WA, USA
    ##   Vancouver, WA 98686, USA
    ##   Clark County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=0,0&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Warning: Reverse geocoding failed with error:
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=46.98429871,-123.7962952&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1250 Pioneer Blvd, Aberdeen, WA 98520, USA
    ##   1421 Clinton St, Aberdeen, WA 98520, USA
    ##   1499 Clinton St, Aberdeen, WA 98520, USA
    ##   1452-1498 Clinton St, Aberdeen, WA 98520, USA
    ##   Aberdeen, WA, USA
    ##   Aberdeen, WA 98520, USA
    ##   Grays Harbor County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.79649353,-78.79810333&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   The Maynard Bridge, 1813 NW Maynard Rd, Cary, NC 27513, USA
    ##   1813 NW Maynard Rd, Cary, NC 27513, USA
    ##   115 High Pine Ct, Cary, NC 27513, USA
    ##   1832 NW Maynard Rd, Cary, NC 27513, USA
    ##   Black Creek Greenway, Cary, NC 27513, USA
    ##   Cary, NC 27513, USA
    ##   Cary, NC, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.70339966,-89.41940308&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   905 Peoria St, Washington, IL 61571, USA
    ##   17 Bondurant St, Washington, IL 61571, USA
    ##   102 Bondurant St, Washington, IL 61571, USA
    ##   1002-904 US-24 BUS, Washington, IL 61571, USA
    ##   Washington, IL, USA
    ##   Washington, IL 61571, USA
    ##   Washington Township, IL, USA
    ##   Tazewell County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=21.23330688,81.63330078&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Vivekanand Park Road, Budhapara, Raipur, Chhattisgarh 492001, India
    ##   Budhapara, Raipur, Chhattisgarh 492001, India
    ##   Raipur, Chhattisgarh 492001, India
    ##   Raipur, Chhattisgarh, India
    ##   Chhattisgarh, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.36830139,-78.09290314&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Goldsboro, NC 27530, USA
    ##   Brogden, NC, USA
    ##   Goldsboro, NC 27530, USA
    ##   Wayne County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.21000671,-96.31529999&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1511 W 24 Hwy, Wamego, KS 66547, USA
    ##   1501 Kaw Valley Park Cir, Wamego, KS 66547, USA
    ##   1048 Kaw Valley Rd, Wamego, KS 66547, USA
    ##   Kaw Valley Rd, Wamego, KS 66547, USA
    ##   Wamego, KS 66547, USA
    ##   Louisville, KS 66547, USA
    ##   Pottawatomie County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.21229553,-110.8789978&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5269 E 18th St, Tucson, AZ 85711, USA
    ##   5315 E 18th St, Tucson, AZ 85711, USA
    ##   843-801 S Charles Ave, Tucson, AZ 85711, USA
    ##   Tucson, AZ 85711, USA
    ##   Tucson, AZ, USA
    ##   Pima County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.74389648,-95.60669708&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2054 S Dairy Ashford Rd, Houston, TX 77077, USA
    ##   S Dairy Ashford Rd, Houston, TX 77077, USA
    ##   Houston, TX 77077, USA
    ##   George Bush Park/Eldridge, Houston, TX, USA
    ##   Houston, TX, USA
    ##   Harris County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.67410278,-86.21040344&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   301 S 26th St, South Bend, IN 46615, USA
    ##   321 S 26th St, South Bend, IN 46615, USA
    ##   26th & Jefferson - Logan Center/Courtyard Apts., South Bend, IN 46615, USA
    ##   311 S 26th St, South Bend, IN 46615, USA
    ##   2699-2601 Birch Way, South Bend, IN 46615, USA
    ##   Swanson Park, South Bend, IN 46615, USA
    ##   South Bend, IN 46615, USA
    ##   Portage Township, IN, USA
    ##   South Bend, IN, USA
    ##   St Joseph County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.25019836,-94.8993988&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   111 E Kansas St, Lansing, KS 66043, USA
    ##   124 N Main St, Lansing, KS 66043, USA
    ##   120 US-73, Lansing, KS 66043, USA
    ##   US-73, Lansing, KS 66043, USA
    ##   Lansing, KS 66043, USA
    ##   Lansing, KS, USA
    ##   Leavenworth County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.16000366,-89.77680206&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8571 Woodland Green Ct, Cordova, TN 38016, USA
    ##   8594 Woodland Green Ct, Cordova, TN 38016, USA
    ##   Cordova Rd, Cordova, TN 38016, USA
    ##   Cordova, TN 38016, USA
    ##   Cordova, Memphis, TN, USA
    ##   Memphis, TN, USA
    ##   Shelby County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.23510742,-84.45819855&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   509 Park Ave, Cincinnati, OH 45215, USA
    ##   Jonte Park, 509 Park Ave, Lockland, OH 45215, USA
    ##   1012 Shepherd Ln, Lockland, OH 45215, USA
    ##   S Leggett Ct, Cincinnati, OH 45215, USA
    ##   Lockland, OH 45215, USA
    ##   Wyoming, OH 45215, USA
    ##   Hamilton County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.4703064,-118.7861023&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   435 Cindy Ln, Fallon, NV 89406, USA
    ##   458 Cindy Ln, Fallon, NV 89406, USA
    ##   700-752 W 4th St, Fallon, NV 89406, USA
    ##   Fallon, NV 89406, USA
    ##   Churchill County, NV, USA
    ##   Nevada, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=17.43339539,78.41110229&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   400, Jawahar Colony, Jubilee Hills, Hyderabad, Telangana 500033, India
    ##   Rd Number 22 B, Jubilee Hills, Hyderabad, Telangana 500033, India
    ##   405, Rd Number 22, Jubilee Hills, Hyderabad, Telangana 500033, India
    ##   Jubilee Hills, Hyderabad, Telangana, India
    ##   Hyderabad, Telangana 500033, India
    ##   Hyderabad, Telangana, India
    ##   Telangana, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.98640442,-76.41649628&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   821 29th St, Newport News, VA 23607, USA
    ##   826 29th St, Newport News, VA 23607, USA
    ##   811 29th St, Newport News, VA 23607, USA
    ##   817 29th St, Newport News, VA 23607, USA
    ##   2999-2901 Marshall Ave, Newport News, VA 23607, USA
    ##   Chestnut, Newport News, VA 23607, USA
    ##   Newport News, VA 23607, USA
    ##   Newport News, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.6558075,-88.22029877&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   12415 248th Ave, Plainfield, IL 60585, USA
    ##   12445 248th Ave, Plainfield, IL 60585, USA
    ##   12417 248th Ave, Plainfield, IL 60585, USA
    ##   248th Ave, Plainfield, IL 60585, USA
    ##   Plainfield, IL 60585, USA
    ##   Wheatland Township, IL, USA
    ##   Will County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.00849915,-117.8135986&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   22930 Golden Springs Dr, Diamond Bar, CA 91765, USA
    ##   Sycamore Canyon Park, 22930 Golden Springs Dr, Diamond Bar, CA 91765, USA
    ##   Sycamore Park, Diamond Bar, CA 91765, USA
    ##   22865 Hilton Head Dr, Diamond Bar, CA 91765, USA
    ##   Diamond Bar, CA, USA
    ##   Diamond Bar, CA 91765, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.42419434,-86.37400055&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   9100 Whitbeck Rd, Montague, MI 49437, USA
    ##   5352 Stanton Blvd, Montague, MI 49437, USA
    ##   9210 Whitbeck Rd, Montague, MI 49437, USA
    ##   9399-9161 Whitbeck Rd, Montague, MI 49437, USA
    ##   Montague, MI, USA
    ##   Montague, MI 49437, USA
    ##   Muskegon County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-37.72380066,145.0744934&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   62 Strathallan Rd, Macleod VIC 3085, Australia
    ##   60 Strathallan Rd, Macleod VIC 3085, Australia
    ##   59 Strathallan Rd, Macleod VIC 3085, Australia
    ##   64-62 Strathallan Rd, Macleod VIC 3085, Australia
    ##   Macleod VIC 3085, Australia
    ##   Macleod West VIC 3085, Australia
    ##   Banyule, VIC, Australia
    ##   Melbourne VIC, Australia
    ##   Victoria, Australia
    ##   Australia
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.36369324,-82.67590332&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8502 Coral Creek Loop, Hudson, FL 34667, USA
    ##   8530 Coral Creek Loop, Hudson, FL 34667, USA
    ##   8921 Hudson Ave, Hudson, FL 34667, USA
    ##   8501 Coral Creek Loop, Hudson, FL 34667, USA
    ##   8699-8501 Regal Ln, Hudson, FL 34667, USA
    ##   Hudson, FL 34667, USA
    ##   Pasco County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.80870056,-95.5515976&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   901 10th Ave, Granite Falls, MN 56241, USA
    ##   1029 9th St, Granite Falls, MN 56241, USA
    ##   900-998 9th St, Granite Falls, MN 56241, USA
    ##   Granite Falls, MN 56241, USA
    ##   Yellow Medicine County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.36410522,-77.46219635&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6186 Murray Terrace, Frederick, MD 21703, USA
    ##   4701 Briggswood Ct, Frederick, MD 21703, USA
    ##   4702-4700 Briggswood Ct, Frederick, MD 21703, USA
    ##   District 23, Ballenger, MD, USA
    ##   Frederick, MD 21703, USA
    ##   Frederick County, MD, USA
    ##   Maryland, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Seneca Plaza, 900 Seneca St, Seattle, WA 98101, USA
    ##   1200 6th Ave, Seattle, WA 98101, USA
    ##   Seneca St & 6th Ave, Seattle, WA 98101, USA
    ##   I-5, Seattle, WA 98101, USA
    ##   Central Business District, Seattle, WA, USA
    ##   Seattle, WA 98101, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.68530273,-72.92960358&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   158 Skyridge Rd, Bristol, CT 06010, USA
    ##   701-737 King Street, Bristol, CT 06010, USA
    ##   Dewitt Dr, Bristol, CT 06010, USA
    ##   87 Moody St, Bristol, CT 06010, USA
    ##   Bristol, CT 06010, USA
    ##   Hartford County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   14615 James St, Holland, MI 49424, USA
    ##   14574 James St, Holland, MI 49424, USA
    ##   2612-2624 Lilac Ave, Holland, MI 49424, USA
    ##   Park Township, MI, USA
    ##   Holland, MI 49424, USA
    ##   Ottawa County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.0993042,-98.58319855&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   900 Kentucky St, Graham, TX 76450, USA
    ##   800-898 Kentucky St, Graham, TX 76450, USA
    ##   Graham, TX 76450, USA
    ##   Young County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.48120117,-88.35540009&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Columbus, MS 39702, USA
    ##   Columbus, MS 39702, USA
    ##   Lowndes County, MS, USA
    ##   Mississippi, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.74679565,-111.8267975&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Canal Corner Pocket Park, 800N N 300 E, Logan, UT 84321, USA
    ##   295 E 800 N, Logan, UT 84321, USA
    ##   811 N 300 E, Logan, UT 84321, USA
    ##   768-798 N 300 E, Logan, UT 84321, USA
    ##   Logan, UT, USA
    ##   Logan, UT 84321, USA
    ##   Cache County, UT, USA
    ##   Utah, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.19630432,-86.271698&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1140 Sherwood Rd, Muskegon, MI 49441, USA
    ##   1146 Sherwood Rd, Muskegon, MI 49441, USA
    ##   3128-3100 Coolidge Rd, Muskegon, MI 49441, USA
    ##   Roosevelt Park, MI 49441, USA
    ##   Muskegon, MI 49441, USA
    ##   Muskegon County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   535 Locust St, Port Orange, FL 32127, USA
    ##   541 Locust St, Port Orange, FL 32127, USA
    ##   500 Locust St, Port Orange, FL 32127, USA
    ##   599-501 Locust St, Port Orange, FL 32127, USA
    ##   PT ORANGE, FL 32127, USA
    ##   Port Orange, FL, USA
    ##   Volusia County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=48.69520569,-122.4123993&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5055 S Samish Way, Bellingham, WA 98229, USA
    ##   5055 Samish Way, Bellingham, WA 98229, USA
    ##   5054 Samish Way, Bellingham, WA 98229, USA
    ##   Bellingham, WA 98229, USA
    ##   Whatcom County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.16969299,-79.39569855&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   205 E Illinois Ave, Southern Pines, NC 28387, USA
    ##   480 S Ashe St, Southern Pines, NC 28387, USA
    ##   420 S Ashe St, Southern Pines, NC 28387, USA
    ##   471 S Ashe St, Southern Pines, NC 28387, USA
    ##   Unnamed Road, United States
    ##   Southern Pines, NC, USA
    ##   Southern Pines, NC 28387, USA
    ##   7, McNeill, NC, USA
    ##   Moore County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.67860413,-82.02629852&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2511 Diplomat Pkwy W, Cape Coral, FL 33993, USA
    ##   2515 NW 14th Terrace, Cape Coral, FL 33993, USA
    ##   2513 Diplomat Pkwy W, Cape Coral, FL 33993, USA
    ##   Diplomat Pkwy W, Cape Coral, FL 33993, USA
    ##   Burnt Store, Cape Coral, FL, USA
    ##   Fort Myers, FL 33993, USA
    ##   Cape Coral, FL, USA
    ##   Lee County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Chidambara Nagar, Kottar, Nagercoil, Tamil Nadu 629001, India
    ##   Tamil Nadu 629001, India
    ##   Nagercoil, Tamil Nadu, India
    ##   Kanyakumari, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   3199 Highland Dr SE, Smyrna, GA 30080, USA
    ##   Highland Drive Park, 3209 Highland Dr SE, Smyrna, GA 30080, USA
    ##   3209 Highland Dr SE, Smyrna, GA 30080, USA
    ##   3099 Jonquil Dr, Smyrna, GA 30080, USA
    ##   Smyrna, GA 30080, USA
    ##   Smyrna, GA, USA
    ##   Cobb County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.08009338,-77.63420105&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1200 Miracle Mile Dr, Rochester, NY 14623, USA
    ##   2375 Marketplace Dr, Rochester, NY 14623, USA
    ##   Marketplace Dr, Rochester, NY 14623, USA
    ##   Rochester, NY 14623, USA
    ##   Henrietta, NY, USA
    ##   Monroe County, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Kennedy Drive at South Burlington High School, South Burlington, VT 05403, USA
    ##   2 Kennedy Dr, South Burlington, VT 05403, USA
    ##   20 Kennedy Dr, South Burlington, VT 05403, USA
    ##   Kennedy Dr, South Burlington, VT 05403, USA
    ##   South Burlington, VT 05403, USA
    ##   South Burlington, VT, USA
    ##   Chittenden County, VT, USA
    ##   Vermont, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   29-99 Barton Rd, Yonkers, NY 10701, USA
    ##   133 Longspur Rd, Yonkers, NY 10701, USA
    ##   77 Barton Rd, Yonkers, NY 10701, USA
    ##   99-1 Victoria Ln, Yonkers, NY 10701, USA
    ##   Bryn Mawr, Yonkers, NY 10701, USA
    ##   Yonkers, NY 10701, USA
    ##   Yonkers, NY, USA
    ##   Westchester County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.96350098,-76.72689819&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   41 E Market St, York, PA 17401, USA
    ##   41 N George St, York, PA 17401, USA
    ##   25 N Court Ave, York, PA 17401, USA
    ##   60 E Clarke Ave, York, PA 17401, USA
    ##   N Court Ave, York, PA 17401, USA
    ##   York, PA 17401, USA
    ##   York, PA, USA
    ##   York County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.6282959,-121.3307037&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Carmichael Park, 3779, 5750 Grant Ave, Carmichael, CA 95608, United States
    ##   6957 Fair Oaks Blvd, Carmichael, CA 95608, USA
    ##   3398 Green Park Ln, Carmichael, CA 95608, USA
    ##   Carmichael Park Rd, Carmichael, CA 95608, USA
    ##   Carmichael, CA 95608, USA
    ##   Carmichael, CA, USA
    ##   Sacramento County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   14212 Banbury Way, Tampa, FL 33624, USA
    ##   Carrollwood Village Phase II, Greater Carrollwood, FL, USA
    ##   Tampa, FL 33624, USA
    ##   Greater Carrollwood, FL, USA
    ##   Hillsborough County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Saunders Park, 3827 Powelton Ave, Philadelphia, PA 19104, USA
    ##   300-50 Saunders Ave, Philadelphia, PA 19104, USA
    ##   329 N 39th St, Philadelphia, PA 19104, USA
    ##   3914-3900 Powelton Ave, Philadelphia, PA 19104, USA
    ##   West Powelton, Philadelphia, PA, USA
    ##   Philadelphia, PA 19104, USA
    ##   Philadelphia, PA, USA
    ##   Philadelphia County, Philadelphia, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   7233 W Kl Ave, Kalamazoo, MI 49009, USA
    ##   7095 W Kl Ave, Kalamazoo, MI 49009, USA
    ##   1076 S 8th St, Kalamazoo, MI 49009, USA
    ##   800-1058 S 8th St, Kalamazoo, MI 49009, USA
    ##   Oshtemo Township, MI, USA
    ##   Kalamazoo, MI 49009, USA
    ##   Kalamazoo County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Davis Playground, 5680 Hobart St, Pittsburgh, PA 15217, USA
    ##   5700 Hobart St, Pittsburgh, PA 15217, USA
    ##   5702 Hobart St, Pittsburgh, PA 15217, USA
    ##   5673 Hobart St, Pittsburgh, PA 15217, USA
    ##   Squirrel Hill South, Pittsburgh, PA, USA
    ##   Pittsburgh, PA 15217, USA
    ##   Pittsburgh, PA, USA
    ##   Allegheny County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-23.47659302,-47.44180298&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Av. São Bernardo do Campo, 170 - Jardim Leocadia, Sorocaba - SP, 18085-310, Brazil
    ##   Ponte Do Pinga-pinga - Rio, Sorocaba - SP, Brazil
    ##   Av. São Bernardo do Campo, 16 - Jardim Leocadia, Sorocaba - SP, 18085-310, Brazil
    ##   Av. Quinze de Agosto - Jardim Leocadia, Sorocaba - SP, 18035-095, Brazil
    ##   Jardim Maria do Carmo, Sorocaba - SP, Brazil
    ##   Sorocaba - State of São Paulo, 18081-101, Brazil
    ##   Sorocaba - State of São Paulo, Brazil
    ##   Sorocaba, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.04750061,-87.89640045&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1333 N Prospect Ave, Milwaukee, WI 53202, USA
    ##   Burns Commons, 1300 N Franklin Pl, Milwaukee, WI 53202, USA
    ##   Burns Commons, Milwaukee, WI 53202, USA
    ##   1312 WI-32, Milwaukee, WI 53202, USA
    ##   1335-1333 WI-32, Milwaukee, WI 53202, USA
    ##   Yankee Hill, Milwaukee, WI 53202, USA
    ##   East Town, Milwaukee, WI 53202, USA
    ##   Milwaukee, WI 53202, USA
    ##   Milwaukee, WI, USA
    ##   Milwaukee County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.70700073,-117.9519043&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Heritage Park, 17641 Los Alamos St, Fountain Valley, CA 92708, USA
    ##   17588 Brookhurst St, Fountain Valley, CA 92708, USA
    ##   17587 Gardens Pl, Fountain Valley, CA 92708, USA
    ##   17698-17600 San Simeon St, Fountain Valley, CA 92708, USA
    ##   Downtown Village, Fountain Valley, CA 92708, USA
    ##   Santa Ana, CA 92708, USA
    ##   Fountain Valley, CA 92708, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.34170532,-86.72119904&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   211A Pear Orchard Dr, Goodlettsville, TN 37072, USA
    ##   Old Springfield Pike, Goodlettsville, TN 37072, USA
    ##   212 Pear Orchard Dr, Goodlettsville, TN 37072, USA
    ##   GOODLETTSVLLE, TN 37072, USA
    ##   Nashville, TN, USA
    ##   Davidson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1377 Massachusetts Ave NW, Washington, DC 20005, USA
    ##   Massachusetts Ave NW, Washington, DC 20005, USA
    ##   Logan Circle, Washington, DC, USA
    ##   Washington, DC 20005, USA
    ##   Downtown, Washington, DC, USA
    ##   Washington, DC, USA
    ##   District of Columbia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   5003 Meadow View Dr, Taylorsville, UT 84123, USA
    ##   Jordan River Parkway Equestrian Trail, Taylorsville, UT 84123, USA
    ##   5022 Meadow View Dr, Taylorsville, UT 84123, USA
    ##   Salt Lake City, UT 84123, USA
    ##   Taylorsville, UT, USA
    ##   Salt Lake Valley, Utah, USA
    ##   Salt Lake County, UT, USA
    ##   Utah, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.68009949,-73.98470306&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3 Av/Butler St, Brooklyn, NY 11217, USA
    ##   269 Douglass St, Brooklyn, NY 11217, USA
    ##   225 Nevins St, Brooklyn, NY 11217, USA
    ##   199 3rd Ave, Brooklyn, NY 11217, USA
    ##   347-285 Douglass St, Brooklyn, NY 11217, USA
    ##   Gowanus, Brooklyn, NY, USA
    ##   Brooklyn, NY 11217, USA
    ##   Brooklyn, NY, USA
    ##   Kings County, Brooklyn, NY, USA
    ##   New York, NY, USA
    ##   Long Island, New York, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.98410034,-77.36720276&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1552 Kingstream Cir, Herndon, VA 20170, USA
    ##   Sugarland Run Trail, Herndon, VA 20170, USA
    ##   1551 Kingstream Cir, Herndon, VA 20170, USA
    ##   Herndon, VA 20170, USA
    ##   Dranesville, VA, USA
    ##   Fairfax County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.01319885,-93.02970123&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1686 Gervais Ave, St Paul, MN 55109, USA
    ##   1679 Gervais Ave, Maplewood, MN 55109, USA
    ##   1666-1686 Gervais Ave, Maplewood, MN 55109, USA
    ##   North St Paul, MN 55109, USA
    ##   Maplewood, MN, USA
    ##   Ramsey County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.01669312,-82.1359024&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   401 N Dort St, Plant City, FL 33563, USA
    ##   Recreation Department-Winter Visitor, 403 N Dort St, Plant City, FL 33563, USA
    ##   401 Oak Ave, Plant City, FL 33563, USA
    ##   Oak Ave, Plant City, FL 33563, USA
    ##   Plant City, FL 33563, USA
    ##   Plant City, FL, USA
    ##   Hillsborough County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Middle Island by field stand, 197 Middle Country Rd, Middle Island, NY 11953, USA
    ##   197 Middle Country Rd, Middle Island, NY 11953, USA
    ##   Unnamed Road, Middle Island, NY 11953, USA
    ##   Middle Island, NY 11953, USA
    ##   Brookhaven, NY, USA
    ##   Long Island, New York, USA
    ##   Suffolk County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.86849976,-85.96900177&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6185 Sunnyside Rd, Indianapolis, IN 46236, USA
    ##   11304-11300 Peacock Dr, Indianapolis, IN 46236, USA
    ##   Oaklandon, IN 46235, USA
    ##   Lawrence, IN, USA
    ##   Lawrence Township, IN, USA
    ##   Marion County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   R. Edmundo Zanoni, 196 - Jardim das Cerejeiras, Atibaia - SP, 12951-030, Brazil
    ##   R. Edmundo Zanoni, 194 - Jardim das Cerejeiras, Atibaia - SP, 12951-030, Brazil
    ##   Cerejeiras III Glebas, Atibaia - SP, Brazil
    ##   R. José de Campos - Casas Populares, Atibaia - SP, 12951-088, Brazil
    ##   Atibaia - State of São Paulo, Brazil
    ##   Atibaia, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.11700439,-85.94429779&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5400 Whitney Woods Rd, Cave City, KY 42127, USA
    ##   Cave City, KY 42127, USA
    ##   Barren County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.75390625,-119.7084961&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5398 E Harvey Ave, Fresno, CA 93727, USA
    ##   796 N Minnewawa Ave, Fresno, CA 93727, USA
    ##   5300-5398 E Harvey Ave, Fresno, CA 93727, USA
    ##   Fresno, CA 93727, USA
    ##   Roosevelt, Fresno, CA, USA
    ##   Fresno, CA, USA
    ##   Fresno County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   12608 Bella Pkwy, Manor, TX 78653, USA
    ##   12691 Old Hwy 20, Manor, TX 78653, USA
    ##   Bella Pkwy, Manor, TX 78653, USA
    ##   Webberville, TX 78653, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   107 Sunset Terrace, Troy, NY 12180, USA
    ##   109 Sunset Terrace, Troy, NY 12180, USA
    ##   Sunset Terrace, Troy, NY 12180, USA
    ##   Troy, NY, USA
    ##   Troy, NY 12180, USA
    ##   Rensselaer County, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1500 Rose Ln, Raleigh, NC 27610, USA
    ##   Dacian Road Park, 566 Dacian Rd, Raleigh, NC 27610, USA
    ##   570 Rose Ln, Raleigh, NC 27610, USA
    ##   Walnut Creek Trail, Raleigh, NC 27610, USA
    ##   570 Dacian Rd, Raleigh, NC 27610, USA
    ##   Southeast Raleigh, Raleigh, NC, USA
    ##   Raleigh, NC, USA
    ##   Raleigh, NC 27610, USA
    ##   Wake County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.95440674,-75.16570282&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Love Park, Arch St, Philadelphia, PA 19102, USA
    ##   1500 Arch St, Philadelphia, PA 19102, USA
    ##   16th St & Arch St - FS, Philadelphia, PA 19102, USA
    ##   1506 Arch St, Philadelphia, PA 19103, USA
    ##   1511-1513 Arch St, Philadelphia, PA 19102, USA
    ##   MIDDLE CITY EAST, PA 19102, USA
    ##   Logan Square, Philadelphia, PA, USA
    ##   Philadelphia, PA, USA
    ##   Philadelphia County, Philadelphia, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   2 Keyser Lane, Amesbury, MA 01913, USA
    ##   98 Friend St, Amesbury, MA 01913, USA
    ##   2 Keyser Ln, Amesbury, MA 01913, USA
    ##   Amesbury, MA, USA
    ##   Amesbury, MA 01913, USA
    ##   Essex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.85499573,-81.67890167&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   625 E McDonald Ave, Eustis, FL 32726, USA
    ##   E McDonald Ave & Salem St, Eustis, FL 32726, USA
    ##   644 E McDonald Ave, Eustis, FL 32726, USA
    ##   215 N Salem St, Eustis, FL 32726, USA
    ##   Eustis, FL, USA
    ##   Eustis, FL 32726, USA
    ##   Lake County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.22059631,-82.28530121&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   State Rte 732, Haysi, VA 24256, USA
    ##   Sand Lick, VA, USA
    ##   Haysi, VA 24256, USA
    ##   Dickenson County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.56390381,-79.71720123&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2564 Dinning Ct, Mississauga, ON L5M 5E7, Canada
    ##   2572 Dinning Ct, Mississauga, ON L5M 5E7, Canada
    ##   5358 Middlebury Dr, Mississauga, ON L5M 5E6, Canada
    ##   5378-5366 Middlebury Dr, Mississauga, ON L5M 5E6, Canada
    ##   Mississauga, ON L5M 5E7, Canada
    ##   Mississauga, ON L5M, Canada
    ##   Erin Mills, Mississauga, ON, Canada
    ##   Mississauga, ON, Canada
    ##   Regional Municipality of Peel, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Multiple addresses found, the first will be returned:
    ##   301-499 Jackson Rd, South Bend, IN 46614, USA
    ##   373 Jackson Rd, South Bend, IN 46614, USA
    ##   Fellows St, South Bend, IN 46614, USA
    ##   Centre Township, IN, USA
    ##   South Bend, IN, USA
    ##   South Bend, IN 46614, USA
    ##   St Joseph County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10701 Hwy 99, Everett, WA 98204, USA
    ##   10700 Evergreen Way, Everett, WA 98204, USA
    ##   108th St SW, Everett, WA 98204, USA
    ##   Twin Creeks, Everett, WA, USA
    ##   Everett, WA 98204, USA
    ##   Everett, WA, USA
    ##   Snohomish County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   3157 Norwood Ave, San Jose, CA 95148, USA
    ##   3155 Norwood Ave, San Jose, CA 95148, USA
    ##   3199-3163 Norwood Ave, San Jose, CA 95148, USA
    ##   Centerwood, San Jose, CA 95148, USA
    ##   San Jose, CA 95148, USA
    ##   San Jose, CA, USA
    ##   Santa Clara County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.85450745,-97.1359024&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   3200 Meadow Park Dr, Bedford, TX 76021, USA
    ##   3005 Meadow Park Dr, Bedford, TX 76021, USA
    ##   2099-2001 Homecraft Dr, Bedford, TX 76021, USA
    ##   Bedford, TX 76021, USA
    ##   Bedford, TX, USA
    ##   Tarrant County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Columbus Park, Mulberry Street &, Baxter St, New York, NY 10013, United States
    ##   95 Bayard St, New York, NY 10013, USA
    ##   78 Baxter St, New York, NY 10013, USA
    ##   35 Baxter St, New York, NY 10013, USA
    ##   New York, NY 10013, USA
    ##   Lower Manhattan, New York, NY, USA
    ##   Manhattan, New York, NY, USA
    ##   New York County, New York, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Mojave Fwy, San Bernardino, CA 92407, USA
    ##   San Bernardino, CA, USA
    ##   DEVORE HGHTS, CA 92407, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=29.52110291,-98.32929993&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8200 Spring Town St, Converse, TX 78109, USA
    ##   Unnamed Road, Converse, TX 78109, USA
    ##   Converse, TX, USA
    ##   Converse, TX 78109, USA
    ##   Northeast Side, Wetmore, TX, USA
    ##   Bexar County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.06820679,-80.2928009&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Bolton Park, 1590 Bolton St SW, Winston-Salem, NC 27103, USA
    ##   Unnamed Road, Winston-Salem, NC 27103, USA
    ##   Winston-Salem, NC 27103, USA
    ##   Winston, NC, USA
    ##   Winston-Salem, NC, USA
    ##   Forsyth County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=11.10499573,77.34658813&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   13, Universal Theater Road, Kannipiran Colony, Valipalayam, Tiruppur, Tamil Nadu 641602, India
    ##   Aroma Hotel Rd, Kannipiran Colony, Valipalayam, Tiruppur, Tamil Nadu 641601, India
    ##   Kannipiran Colony, Valipalayam, Tiruppur, Tamil Nadu, India
    ##   Valipalayam, Tiruppur, Tamil Nadu, India
    ##   Tiruppur, Tamil Nadu 641602, India
    ##   Tiruppur, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   3007 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   3702 Quarter Horse Dr, Yorba Linda, CA 92886, USA
    ##   S Ridge Trail, Yorba Linda, CA 92886, USA
    ##   Yorba Linda, CA 92886, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.4420929,-97.6339035&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1215 Noton Ct, Pflugerville, TX 78660, USA
    ##   1299 Noton Ct, Pflugerville, TX 78660, USA
    ##   Settlers Valley Trail, Pflugerville, TX 78660, USA
    ##   Creekside Park, 418 Settlers Valley Dr, Pflugerville, TX 78660, USA
    ##   Wells Point Phase C, Pflugerville, TX 78660, USA
    ##   Pflugerville, TX, USA
    ##   Pflugerville, TX 78660, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   R. Abraão Miguel do Carmo, 548 - Vila Monte Alegre, São Paulo - SP, 04306-090, Brazil
    ##   Av. Afonso D'Escragnolle Taunay, 3972 - Vila Monte Alegre, São Paulo - SP, Brazil
    ##   R. Abraão Miguel do Carmo, São Paulo - SP, Brazil
    ##   Vila Monte Alegre, São Paulo - SP, Brazil
    ##   São Paulo - State of São Paulo, Brazil
    ##   São Paulo, State of São Paulo, Brazil
    ##   State of São Paulo, Brazil
    ##   Brazil
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.58180237,-87.41619873&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   184 Bob White Dr, Clarksville, TN 37042, USA
    ##   TN-374, Clarksville, TN 37042, USA
    ##   3 Arrowood Dr, Clarksville, TN 37042, USA
    ##   101 Bob White Dr, Clarksville, TN 37042, USA
    ##   Clarksville, TN 37042, USA
    ##   Clarksville, TN, USA
    ##   Montgomery County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.02400208,-84.23960114&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   390 Waters Bend Way, Alpharetta, GA 30022, USA
    ##   659 Falls Lake Dr, Johns Creek, GA 30022, USA
    ##   501-599 Falls Watch Cir, Johns Creek, GA 30022, USA
    ##   Alpharetta, GA 30022, USA
    ##   Johns Creek, GA, USA
    ##   Fulton County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.08120728,-89.3844986&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   300 E Gorham St, Madison, WI 53703, USA
    ##   E Gorham & N Hancock (WB), Madison, WI 53706, USA
    ##   311 N Hancock St, Madison, WI 53703, USA
    ##   474 E Gorham St, Madison, WI 53703, USA
    ##   301-399 N Franklin St, Madison, WI 53703, USA
    ##   Madison, WI 53706, USA
    ##   Madison, WI, USA
    ##   Dane County, WI, USA
    ##   Wisconsin, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.87399292,-71.38439941&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   33 Taft St, Pawtucket, RI 02860, USA
    ##   37 Taft St, Pawtucket, RI 02860, USA
    ##   88 Pleasant St, Pawtucket, RI 02860, USA
    ##   I-95, Pawtucket, RI 02860, USA
    ##   Pawtucket, RI 02860, USA
    ##   Pawtucket, RI, USA
    ##   Providence County, RI, USA
    ##   Rhode Island, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   8556 Sandstone Way, Manassas Park, VA 20111, USA
    ##   8601 Centreville Rd, Manassas, VA 20111, USA
    ##   8611-8603 Centreville Rd, Manassas, VA 20110, USA
    ##   Manassas Park, VA 20111, USA
    ##   Brentsville, VA, USA
    ##   Prince William County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Ninnescah, KS, USA
    ##   PRETTY PRAIRE, KS 67570, USA
    ##   Reno County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.56619263,-79.70780182&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   820 McAllister Dr, Lower Burrell, PA 15068, USA
    ##   Cherry Ln, Lower Burrell, PA 15068, USA
    ##   3099 Cherry Ln, Lower Burrell, PA 15068, USA
    ##   Lower Burrell, PA 15068, USA
    ##   NEW KENSINGTN, PA 15068, USA
    ##   Westmoreland County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   223 Macalester St, St Paul, MN 55105, USA
    ##   St Clair Ave & Macalester St, St Paul, MN 55105, USA
    ##   1600 Grand Ave, St Paul, MN 55105, USA
    ##   Unnamed Road, St Paul, MN 55105, USA
    ##   Macalester - Groveland, St Paul, MN, USA
    ##   St Paul, MN 55105, USA
    ##   St Paul, MN, USA
    ##   Ramsey County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   200 Newmantown Rd, Grovetown, GA 30813, USA
    ##   208-1/2 Newmantown Rd, Grovetown, GA 30813, USA
    ##   104 Old Berzelia Rd, Grovetown, GA 30813, USA
    ##   Spring St, Grovetown, GA 30813, USA
    ##   Grovetown, GA 30813, USA
    ##   Columbia County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   7233 W Kl Ave, Kalamazoo, MI 49009, USA
    ##   7095 W Kl Ave, Kalamazoo, MI 49009, USA
    ##   1076 S 8th St, Kalamazoo, MI 49009, USA
    ##   800-1058 S 8th St, Kalamazoo, MI 49009, USA
    ##   Oshtemo Township, MI, USA
    ##   Kalamazoo, MI 49009, USA
    ##   Kalamazoo County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.80149841,-79.35769653&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   12 Wellesbourne Crescent, North York, ON M2H 1Y7, Canada
    ##   7 Wellesbourne Crescent, North York, ON M2H 1Y6, Canada
    ##   15 Wellesbourne Crescent, North York, ON M2H 1Y6, Canada
    ##   Duncan Creek Trail, North York, ON M2H 3J7, Canada
    ##   North York, ON M2H 1Y7, Canada
    ##   Hillcrest Village, Toronto, ON, Canada
    ##   North York, ON M2H, Canada
    ##   North York, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.44459534,-122.1835022&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Jack W. Lyle Park, 640 Fremont St, Menlo Park, CA 94025, USA
    ##   500 Arbor Rd, Menlo Park, CA 94025, USA
    ##   667 Fremont St, Menlo Park, CA 94025, USA
    ##   699-649 Fremont St, Menlo Park, CA 94025, USA
    ##   West Menlo Park, CA 94025, USA
    ##   Menlo Park, CA, USA
    ##   San Francisco Peninsula, California, USA
    ##   San Mateo County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.33610535,-87.78970337&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   116 E Lincoln Ave, Peotone, IL 60468, USA
    ##   127 E Crawford St, Peotone, IL 60468, USA
    ##   301 Washington St, Peotone, IL 60468, USA
    ##   315 Washington St, Peotone, IL 60468, USA
    ##   Washington St, Peotone, IL 60468, USA
    ##   Peotone, IL 60468, USA
    ##   Peotone Township, IL, USA
    ##   Will County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.09080505,-77.43479919&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   40 Winding Brook Dr, Fairport, NY 14450, USA
    ##   26 Misty Pine Rd, Fairport, NY 14450, USA
    ##   41 Winding Brook Dr, Fairport, NY 14450, USA
    ##   Winding Brook Dr, Fairport, NY 14450, USA
    ##   Fairport, NY 14450, USA
    ##   Perinton, NY, USA
    ##   Monroe County, NY, USA
    ##   New York, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10115 NE Hwy 99, Vancouver, WA 98686, USA
    ##   10127 NE Hwy 99, Vancouver, WA 98686, USA
    ##   NE Hwy 99, Vancouver, WA 98686, USA
    ##   Salmon Creek, WA, USA
    ##   Pleasant Valley, Battle Ground, WA, USA
    ##   Vancouver, WA 98686, USA
    ##   Clark County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.09289551,-72.52739716&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   23 Emerson St, Springfield, MA 01118, USA
    ##   27 Emerson St, Springfield, MA 01118, USA
    ##   East Forest Park, Springfield, MA, USA
    ##   Springfield, MA 01118, USA
    ##   Springfield, MA, USA
    ##   Hampden County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.92610168,-71.30110168&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   55 Edgecliff Ave, Attleboro, MA 02703, USA
    ##   77 Woodcrest Dr, Attleboro, MA 02703, USA
    ##   57 Edgecliff Ave, Attleboro, MA 02703, USA
    ##   69-79 Edgecliff Ave, Attleboro, MA 02703, USA
    ##   South Attleboro, MA 02703, USA
    ##   Attleboro, MA, USA
    ##   Bristol County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   15940 Bernardo Heights Pkwy, San Diego, CA 92128, USA
    ##   16066 Bernardo Heights Pkwy, San Diego, CA 92128, USA
    ##   Bernardo Heights Pkwy, San Diego, CA 92128, USA
    ##   San Diego, CA 92128, USA
    ##   Rancho Bernardo, San Diego, CA, USA
    ##   San Diego, CA, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Seattle Japanese Garden, 1075 Lake Washington Blvd E, Seattle, WA 98112, USA
    ##   1195 Lake Washington Blvd E, Seattle, WA 98112, USA
    ##   1219-1201 Lake Washington Blvd E, Seattle, WA 98112, USA
    ##   Stevens, Seattle, WA, USA
    ##   Seattle, WA 98112, USA
    ##   Seattle, WA, USA
    ##   King County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Johnson City, KS 67855, USA
    ##   Stanton, KS, USA
    ##   Johnson City, KS 67855, USA
    ##   Stanton County, KS, USA
    ##   Kansas, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.21330261,-97.853302&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7806 Nairn Dr, Austin, TX 78749, USA
    ##   7804 Nairn Dr, Austin, TX 78749, USA
    ##   7808 Nairn Dr, Austin, TX 78749, USA
    ##   Unnamed Road, Austin, TX 78749, USA
    ##   Dick Nichols District Park, 8011 Beckett Rd, Austin, TX 78749, USA
    ##   Maple Run, Austin, TX 78749, USA
    ##   Austin, TX 78749, USA
    ##   Austin, TX, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   10055 Monte Vista Ave, Montclair, CA 91763, USA
    ##   4900 Orchard St, Montclair, CA 91763, USA
    ##   4937 Denver St, Montclair, CA 91763, USA
    ##   9982-10026 Monte Vista Ave, Montclair, CA 91763, USA
    ##   Montclair, CA 91763, USA
    ##   Montclair, CA, USA
    ##   San Bernardino County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=22.55250549,72.9552002&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Swaminarayan Society Rd, Mathiya Chora, Anand, Gujarat 388001, India
    ##   Mathiya Chora, Anand, Gujarat, India
    ##   Gujarat 388001, India
    ##   Anand, Gujarat, India
    ##   Gujarat, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   Lamplighter Park, 39 Enchanted, Irvine, CA 92620, USA
    ##   42 Enchanted, Irvine, CA 92620, USA
    ##   160 Vintage, Irvine, CA 92620, USA
    ##   Vintage, Irvine, CA 92620, USA
    ##   Woodbury, Irvine, CA 92620, USA
    ##   Irvine, CA 92620, USA
    ##   Irvine, CA, USA
    ##   Orange County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.9571991,-74.16040039&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   50 1st Ave, Paterson, NJ 07514, USA
    ##   240 Bamford Ave, Hawthorne, NJ 07506, USA
    ##   225-239 Bamford Ave, Hawthorne, NJ 07506, USA
    ##   Goffle Brook Park, 788 Lafayette Ave, Hawthorne, NJ 07506, USA
    ##   Hawthorne, NJ 07506, USA
    ##   Hawthorne, NJ, USA
    ##   Passaic County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=22.29089355,114.1499939&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Hong Kong Macau Ferry Terminal, 168-200 Connaught Rd Central, Sheung Wan, Hong Kong
    ##   Hong Kong (Sheung Wan), Sheung Wan, Hong Kong
    ##   8 Western Fire Services St, Sheung Wan, Hong Kong
    ##   Western Harbour Crossing, Hong Kong
    ##   Hong Kong
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=28.57350159,77.32080078&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   A-41A, Block A, Sector 17, Noida, Uttar Pradesh 201301, India
    ##   Unnamed Road, BHEL Township,Noida, Block A, Sector 17, Noida, Uttar Pradesh 201301, India
    ##   Block A, Sector 17, Noida, Uttar Pradesh 201301, India
    ##   Sector 17, Noida, Uttar Pradesh 201301, India
    ##   Uttar Pradesh 201301, India
    ##   Noida, Uttar Pradesh, India
    ##   Gautam Buddh Nagar, Uttar Pradesh, India
    ##   Uttar Pradesh, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   26716 Palmetto Lake Ct W, Denham Springs, LA 70726, USA
    ##   11356 Palmetto Lake Ave, Denham Springs, LA 70726, USA
    ##   Palmetto Ct W, Denham Springs, LA 70726, USA
    ##   5, LA, USA
    ##   Denham Springs, LA 70726, USA
    ##   Livingston Parish, LA, USA
    ##   Louisiana, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   821 29th St, Newport News, VA 23607, USA
    ##   826 29th St, Newport News, VA 23607, USA
    ##   811 29th St, Newport News, VA 23607, USA
    ##   817 29th St, Newport News, VA 23607, USA
    ##   2999-2901 Marshall Ave, Newport News, VA 23607, USA
    ##   Chestnut, Newport News, VA 23607, USA
    ##   Newport News, VA 23607, USA
    ##   Newport News, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.56300354,-84.22879791&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   60 Sycamore Creek Dr, Springboro, OH 45066, USA
    ##   64 Sycamore Creek Dr, Springboro, OH 45066, USA
    ##   98-2 Sycamore Creek Ct, Springboro, OH 45066, USA
    ##   Springboro, OH, USA
    ##   Springboro, OH 45066, USA
    ##   Clearcreek Township, OH, USA
    ##   Warren County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   21 Harrison Ave, Woburn, MA 01801, USA
    ##   25 Harrison Ave, Woburn, MA 01801, USA
    ##   20 Harrison Ave, Woburn, MA 01801, USA
    ##   Abbott St, Woburn, MA 01801, USA
    ##   Woburn, MA 01801, USA
    ##   Woburn, MA, USA
    ##   Middlesex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.54490662,-74.35169983&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   270 Highland Ave, Metuchen, NJ 08840, USA
    ##   136 Grove Ave, Metuchen, NJ 08840, USA
    ##   100 Oakland Ave, Metuchen, NJ 08840, USA
    ##   Centennial Park, Grove Ave & Oakland Ave, Metuchen, NJ 08840, United States
    ##   264-280 Highland Ave, Metuchen, NJ 08840, USA
    ##   Metuchen, NJ 08840, USA
    ##   Middlesex County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=55.75270081,37.61720276&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Zhitnitskaya Ulitsa, Moskva, Russia, 109012
    ##   Moscow, Russia, 109012
    ##   Moscow Kremlin, Moscow, Russia
    ##   Tverskoy District, Moscow, Russia
    ##   Tverskoy, Moscow, Russia
    ##   Central Administrative Okrug, Moscow, Russia
    ##   Moscow, Russia
    ##   Russia
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.93280029,-60.64379883&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   47 Anslum Rd, Eskasoni, NS B1W 1A4, Canada
    ##   22 Castle Bay Rd, Eskasoni, NS B1W 1A1, Canada
    ##   7 Castle Bay Rd, Eskasoni, NS, Canada
    ##   5086-5130 Shore Rd, Christmas Island, NS B1T 1K5, Canada
    ##   Eskasoni, NS B1W 1A4, Canada
    ##   Eskasoni, NS B1W, Canada
    ##   Eskasoni, NS, Canada
    ##   Cape Breton Island, Nova Scotia, Canada
    ##   Cape Breton Regional Municipality, NS, Canada
    ##   Nova Scotia, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.52400208,-82.51629639&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1280 Bridwell St, Kingsport, TN 37664, USA
    ##   2516 Nathan St, Kingsport, TN 37664, USA
    ##   1215 Bridwell St, Kingsport, TN 37664, USA
    ##   2699-2601 Nathan St, Kingsport, TN 37664, USA
    ##   Kingsport, TN 37664, USA
    ##   Kingsport, TN, USA
    ##   Sullivan County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1050 Kimbark St, Longmont, CO 80501, USA
    ##   440 11th Ave, Longmont, CO 80501, USA
    ##   1053 Kimbark St, Longmont, CO 80501, USA
    ##   1199-1101 Kimbark St, Longmont, CO 80501, USA
    ##   Kiteley, Longmont, CO 80501, USA
    ##   Longmont, CO 80501, USA
    ##   Longmont, CO, USA
    ##   Boulder County, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   188, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Samarth Hanuman Path, Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Ghodapdeo, Byculla East, Byculla, Mumbai, Maharashtra 400033, India
    ##   Byculla East, Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra 400033, India
    ##   Byculla, Mumbai, Maharashtra, India
    ##   Mumbai, Maharashtra, India
    ##   Maharashtra, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   5605 Park Side Rd, Hoover, AL 35244, USA
    ##   Oak Mountain Lake Rd, Birmingham, AL 35242, USA
    ##   5603 Oak Mountain Lake Rd, Birmingham, AL 35242, USA
    ##   Pelham, AL, USA
    ##   Birmingham, AL 35242, USA
    ##   Shelby County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   400, Jawahar Colony, Jubilee Hills, Hyderabad, Telangana 500033, India
    ##   Rd Number 22 B, Jubilee Hills, Hyderabad, Telangana 500033, India
    ##   405, Rd Number 22, Jubilee Hills, Hyderabad, Telangana 500033, India
    ##   Jubilee Hills, Hyderabad, Telangana, India
    ##   Hyderabad, Telangana 500033, India
    ##   Hyderabad, Telangana, India
    ##   Telangana, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.29310608,-83.25479889&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   22340 Columbia St, Dearborn, MI 48124, USA
    ##   22327 Columbia St, Dearborn, MI 48124, USA
    ##   Dearborn, MI 48124, USA
    ##   Dearborn, MI, USA
    ##   Wayne County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   7301 Cliff Ave, Sioux Falls, SD 57108, USA
    ##   47510 85th St, Sioux Falls, SD 57108, USA
    ##   26991 Cliff Ave, Sioux Falls, SD 57108, USA
    ##   27026-27000 Co Hwy 123, Sioux Falls, SD 57108, USA
    ##   Springdale Township, SD, USA
    ##   Sioux Falls, SD 57108, USA
    ##   Lincoln County, SD, USA
    ##   South Dakota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=55.1302948,-118.7946014&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   5306 100 St, Grande Prairie, AB T8W 2R6, Canada
    ##   100 St, Grovedale, AB T0H 1X0, Canada
    ##   5306 Range Rd 61, Grovedale, AB T0H 1X0, Canada
    ##   Grande Prairie, AB, Canada
    ##   Grovedale, AB T0H 1X0, Canada
    ##   Division No. 19, AB, Canada
    ##   Goodfare, AB T0H, Canada
    ##   Alberta, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.83079529,-92.93930054&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8193 Ideal Ave S, Cottage Grove, MN 55016, USA
    ##   8301 81st Ln, Cottage Grove, MN 55016, USA
    ##   8205 Ideal Ave S, Cottage Grove, MN 55016, USA
    ##   Cottage Grove, MN 55016, USA
    ##   Cottage Grove, MN, USA
    ##   Washington County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   3002 Armstrong St, San Diego, CA 92111, USA
    ##   6948 Park Mesa Way, San Diego, CA 92111, USA
    ##   Ciota's Way, San Diego, CA 92111, USA
    ##   Linda Vista, San Diego, CA, USA
    ##   San Diego, CA 92111, USA
    ##   San Diego, CA, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.41740417,-74.60980225&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Cony St, Stamford, NY 12167, USA
    ##   64 River St, Stamford, NY 12167, USA
    ##   Stamford, NY 12167, USA
    ##   Stamford, NY, USA
    ##   Delaware County, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.15910339,-85.21820068&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6103 Middle Valley Rd, Hixson, TN 37343, USA
    ##   4030 Kamin Rd, Hixson, TN 37343, USA
    ##   6020-6298 Middle Valley Rd, Hixson, TN 37343, USA
    ##   Hixson, Chattanooga, TN, USA
    ##   Hixson, TN 37343, USA
    ##   Chattanooga, TN, USA
    ##   Hamilton County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.65609741,-75.2335968&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   202-270 Berger Rd, Glendon, PA 18042, USA
    ##   250 Berger Rd, Easton, PA 18042, USA
    ##   241 Berger Rd, Glendon, PA 18042, USA
    ##   Wottring Mill Rd, Williams Township, PA 18042, USA
    ##   Williams Township, PA, USA
    ##   Williams Township, PA 18042, USA
    ##   Northampton County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   36 Cobb Rd, Ashburnham, MA 01430, USA
    ##   122 Lake Rd, Ashburnham, MA 01430, USA
    ##   Unnamed Road, Ashburnham, MA 01430, USA
    ##   Ashburnham, MA 01430, USA
    ##   Ashburnham, MA, USA
    ##   Worcester County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Computer Science, Loop Rd, Staten Island, NY 10314, USA
    ##   Loop Rd, Staten Island, NY 10314, USA
    ##   Staten Island, NY 10314, USA
    ##   Mid Island, Staten Island, NY, USA
    ##   Richmond County, Staten Island, NY, USA
    ##   Staten Island, NY, USA
    ##   New York, NY, USA
    ##   New York, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.79519653,-84.32479858&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   FM Building - H (Steam Plant), Atlanta, GA 30322, USA
    ##   3 Eagle Row, Atlanta, GA 30322, USA
    ##   Facilities Management Dr, Atlanta, GA 30322, USA
    ##   Atlanta, GA 30322, USA
    ##   Druid Hills, GA, USA
    ##   Dekalb County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.01280212,-88.09670258&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   617 Boxwood Dr, Schaumburg, IL 60193, USA
    ##   703 Duxbury Ln, Schaumburg, IL 60193, USA
    ##   630-798 Grace Ln, Schaumburg, IL 60193, USA
    ##   Schaumburg, IL 60193, USA
    ##   Schaumburg, IL, USA
    ##   Schaumburg Township, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.21040344,-74.82779694&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   866 Big Oak Rd, Morrisville, PA 19067, USA
    ##   870 Roelofs Rd, Morrisville, PA 19067, USA
    ##   901 Roelofs Rd, Morrisville, PA 19067, USA
    ##   Lower Makefield Township, PA, USA
    ##   Yardley, PA 19067, USA
    ##   Bucks County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.26600647,-74.521698&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   201 S Main St, Hightstown, NJ 08520, USA
    ##   156 E Ward St, Hightstown, NJ 08520, USA
    ##   169-163 E Ward St, Hightstown, NJ 08520, USA
    ##   Hightstown, NJ 08520, USA
    ##   Mercer County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.39860535,-71.24510193&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   192 Jericho Hill Rd, Waltham, MA 02451, USA
    ##   329 Lincoln St, Waltham, MA 02451, USA
    ##   298 Jericho Hill Rd, Waltham, MA 02451, USA
    ##   87-299 Jericho Hill Rd, Waltham, MA 02451, USA
    ##   Piety Corner, Waltham, MA, USA
    ##   Waltham, MA 02451, USA
    ##   Waltham, MA, USA
    ##   Middlesex County, MA, USA
    ##   Massachusetts, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.07400513,-118.2611008&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   898 Glendale Blvd, Los Angeles, CA 90026, USA
    ##   Glendale / Santa Ynez, Los Angeles, CA 90026, USA
    ##   850 Glendale Blvd, Los Angeles, CA 90026, USA
    ##   899-831 Glendale Blvd, Los Angeles, CA 90026, USA
    ##   Echo Park, 1632 Bellevue Ave, Los Angeles, CA 90026, USA
    ##   Echo Park, Los Angeles, CA, USA
    ##   Los Angeles, CA 90026, USA
    ##   Los Angeles, CA, USA
    ##   Los Angeles County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.07110596,-86.71959686&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4612 US-41A, Nashville, TN 37211, USA
    ##   4608 Nolensville Pike, Nashville, TN 37211, USA
    ##   4430 Taylor Rd, Nashville, TN 37211, USA
    ##   Wales Dr, Nashville, TN 37211, USA
    ##   Nashville, TN 37211, USA
    ##   Nashville, TN, USA
    ##   Davidson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.80870056,-91.11699677&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1418 Smith St, Burlington, IA 52601, USA
    ##   200 S Gunnison St, Burlington, IA 52601, USA
    ##   Smith St and S Marshall St, Burlington, IA 52601, USA
    ##   135 S Marshall St, Burlington, IA 52601, USA
    ##   1457 Smith St, Burlington, IA 52601, USA
    ##   298-200 S Gunnison St, Burlington, IA 52601, USA
    ##   Burlington, IA, USA
    ##   Burlington, IA 52601, USA
    ##   Des Moines County, IA, USA
    ##   Iowa, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.87980652,-87.62850189&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   152 S State St, Chicago, IL 60603, USA
    ##   Adams & State, Chicago, IL 60603, USA
    ##   3 W Marble Pl, Chicago, IL 60603, USA
    ##   S State St, Chicago, IL 60603, USA
    ##   Chicago, IL 60603, USA
    ##   Chicago Loop, Chicago, IL, USA
    ##   Chicago, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.78930664,-83.71350098&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   301 S Leroy St, Fenton, MI 48430, USA
    ##   711 Davis St, Fenton, MI 48430, USA
    ##   799 Davis St, Fenton, MI 48430, USA
    ##   700-798 Davis St, Fenton, MI 48430, USA
    ##   Fenton, MI, USA
    ##   Fenton, MI 48430, USA
    ##   Genesee County, MI, USA
    ##   Michigan, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.02490234,-84.95770264&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   GA-411, LaGrange, GA 30241, USA
    ##   594 Callaway Church Rd, LaGrange, GA 30241, USA
    ##   LaGrange, GA, USA
    ##   LaGrange, GA 30241, USA
    ##   Troup County, GA, USA
    ##   Georgia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.29930115,-73.9890976&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Cherry street park, Cherry St, Long Branch, NJ 07740, USA
    ##   175 Cherry St, Long Branch, NJ 07740, USA
    ##   145 Cherry St, Long Branch, NJ 07740, USA
    ##   Long Branch, NJ 07740, USA
    ##   Monmouth County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   11348 Lakeview Dr, New Port Richey, FL 34654, USA
    ##   11336 Lakeview Dr, New Port Richey, FL 34654, USA
    ##   11355 Lakeview Dr, New Port Richey, FL 34654, USA
    ##   The Reserve At Golden Acres, FL 34654, USA
    ##   NEW PRT RCHY, FL 34654, USA
    ##   Pasco County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   158 Skyridge Rd, Bristol, CT 06010, USA
    ##   701-737 King Street, Bristol, CT 06010, USA
    ##   Dewitt Dr, Bristol, CT 06010, USA
    ##   87 Moody St, Bristol, CT 06010, USA
    ##   Bristol, CT 06010, USA
    ##   Hartford County, CT, USA
    ##   Connecticut, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.23039246,-97.72429657&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4500 Siringo Pass, Austin, TX 78741, USA
    ##   2209 Pleasant Valley/Sheringham, Austin, TX 78741, USA
    ##   10 Sheringham Dr, Austin, TX 78741, USA
    ##   2321 S Pleasant Valley Rd, Austin, TX 78741, USA
    ##   Pleasant Valley, Austin, TX 78741, USA
    ##   Austin, TX 78741, USA
    ##   Austin, TX, USA
    ##   Travis County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.50999451,-73.5664978&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   6 Boulevard de Maisonneuve O, Montréal, QC H2X, Canada
    ##   Maisonneuve Blvd W, Montreal, QC H2X, Canada
    ##   Quartier des Spectacles, Montreal, QC, Canada
    ##   Montreal, QC H2X, Canada
    ##   Ville-Marie, Montreal, QC, Canada
    ##   Montreal, QC, Canada
    ##   Island of Montreal, Quebec, Canada
    ##   Quebec, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.83779907,-106.538002&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Irvin J Lamka Park, 660 Cloudview Dr, El Paso, TX 79912, USA
    ##   245 Colina Alta Dr, El Paso, TX 79912, USA
    ##   263 Colina Alta Dr, El Paso, TX 79912, USA
    ##   6401-6505 Cloudview Dr, El Paso, TX 79912, USA
    ##   Lambka Park, El Paso, TX 79912, USA
    ##   El Paso, TX 79912, USA
    ##   El Paso, TX, USA
    ##   El Paso County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Margaret Hunt Hill Bridge, Margaret Hunt Hill Bridge, Dallas, TX 75207, USA
    ##   Trinity Skyline Trail, Dallas, TX 75207, USA
    ##   1001 Continental St Via, Dallas, TX 75212, USA
    ##   Dallas, TX 75207, USA
    ##   Dallas, TX, USA
    ##   Dallas County, TX, USA
    ##   Texas, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   535 Locust St, Port Orange, FL 32127, USA
    ##   541 Locust St, Port Orange, FL 32127, USA
    ##   500 Locust St, Port Orange, FL 32127, USA
    ##   599-501 Locust St, Port Orange, FL 32127, USA
    ##   PT ORANGE, FL 32127, USA
    ##   Port Orange, FL, USA
    ##   Volusia County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=26.82380676,-80.14070129&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1018 Diamond Head Way, Palm Beach Gardens, FL 33418, USA
    ##   1074 Diamond Head Way, Palm Beach Gardens, FL 33418, USA
    ##   Riviera Beach, FL 33418, USA
    ##   Palm Beach Gardens, FL, USA
    ##   Palm Beach County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Hollis Park, 3421 S Kenneth Pl, Tempe, AZ 85282, USA
    ##   3466 S Kenneth Pl, Tempe, AZ 85282, USA
    ##   1201-1299 E Laguna Dr, Tempe, AZ 85282, USA
    ##   Tempe, AZ 85282, USA
    ##   South Tempe, Tempe, AZ, USA
    ##   Tempe, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.92179871,-75.28759766&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   24 W Providence Rd, Aldan, PA 19018, USA
    ##   10 W Providence Rd, Aldan, PA 19018, USA
    ##   Providence Park, 10 W Providence Rd, Aldan, PA 19018, USA
    ##   35 W Providence Rd, Aldan, PA 19018, USA
    ##   98-26 W Providence Rd, Aldan, PA 19018, USA
    ##   Aldan, PA, USA
    ##   Clifton Heights, PA 19018, USA
    ##   Delaware County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.54829407,-80.25109863&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   27 Cardigan St, Guelph, ON N1H 7V6, Canada
    ##   150 Woolwich St, Guelph, ON N1H 3V3, Canada
    ##   146 Woolwich St, Guelph, ON N1H, Canada
    ##   50-20 Cardigan St, Guelph, ON N1H, Canada
    ##   Guelph, ON N1H 7V6, Canada
    ##   Guelph, ON N1H, Canada
    ##   Guelph, ON, Canada
    ##   Wellington County, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.167099,-86.78610229&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   755 US-41, Nashville, TN 37219, USA
    ##   US-41, Nashville, TN 37219, USA
    ##   North Capitol, Nashville, TN, USA
    ##   Nashville, TN 37219, USA
    ##   Nashville, TN, USA
    ##   Davidson County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   8532 Wendy Ln E, West Palm Beach, FL 33411, USA
    ##   8034 7th Pl S, West Palm Beach, FL 33411, USA
    ##   FL-91, West Palm Beach, FL 33413, USA
    ##   8001 7th Pl S, West Palm Beach, FL 33411, USA
    ##   West Palm Beach, FL 33411, USA
    ##   Palm Beach County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.65910339,-79.46260071&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Glenlake Square, 215 Glenlake Ave, Toronto, ON M6P, Canada
    ##   1018 Keele St, Toronto, ON M6P, Canada
    ##   183 Keele St, Toronto, ON M6P 2K1, Canada
    ##   200 Keele St, Toronto, ON M6P, Canada
    ##   High Park North, Toronto, ON, Canada
    ##   Toronto, ON M6P, Canada
    ##   Old Toronto, Toronto, ON, Canada
    ##   Toronto, ON, Canada
    ##   Toronto Division, ON, Canada
    ##   Ontario, Canada
    ##   Canada
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=32.37049866,-90.17459869&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   290 Camero Dr, Jackson, MS 39206, USA
    ##   299 Camero Dr, Jackson, MS 39206, USA
    ##   210-298 Camero Dr, Jackson, MS 39206, USA
    ##   Jackson, MS 39206, USA
    ##   Jackson, MS, USA
    ##   Hinds County, MS, USA
    ##   Mississippi, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.10969543,-117.0670013&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1554 S Juniper St, Escondido, CA 92025, USA
    ##   Unnamed Road, Escondido, CA 92025, USA
    ##   Central Escondido, Escondido, CA, USA
    ##   Escondido, CA 92025, USA
    ##   Escondido, CA, USA
    ##   San Diego County, CA, USA
    ##   California, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=35.47399902,-80.87290192&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   19116 Statesville Rd, Cornelius, NC 28031, USA
    ##   19062 Statesville Rd, Cornelius, NC 28031, USA
    ##   19126 Statesville Rd, Cornelius, NC 28031, USA
    ##   20327 Willow Pond Rd, Cornelius, NC 28031, USA
    ##   19801-19899 Pinyon Dr, Cornelius, NC 28031, USA
    ##   Cornelius, NC, USA
    ##   Cornelius, NC 28031, USA
    ##   Lemley, NC, USA
    ##   Mecklenburg County, NC, USA
    ##   North Carolina, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.84829712,-87.65170288&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1140 W 25th St, Chicago, IL 60608, USA
    ##   2553 S Hillock Ave, Chicago, IL 60608, USA
    ##   2472-2518 S Hillock Ave, Chicago, IL 60608, USA
    ##   Pilsen, Chicago, IL, USA
    ##   Chicago, IL 60608, USA
    ##   Chicago, IL, USA
    ##   Cook County, IL, USA
    ##   Illinois, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.26530457,-85.39920044&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2427 Headland Ave, Dothan, AL 36303, USA
    ##   Dothan, AL 36303, USA
    ##   Dothan, AL, USA
    ##   Houston County, AL, USA
    ##   Alabama, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.05349731,-83.01869965&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   33 E Dominion Blvd, Columbus, OH 43214, USA
    ##   40 E Dominion Blvd, Columbus, OH 43214, USA
    ##   4516 N High St, Columbus, OH 43214, USA
    ##   Desantis Dr, Columbus, OH 43214, USA
    ##   Indian Springs, Columbus, OH 43214, USA
    ##   Columbus, OH 43214, USA
    ##   Columbus, OH, USA
    ##   Franklin County, OH, USA
    ##   Ohio, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.90859985,-86.1210022&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8420 Woodfield Crossing Blvd, Indianapolis, IN 46240, USA
    ##   8440 Woodfield Crossing Blvd, Indianapolis, IN 46240, USA
    ##   8466 Woodfield Crossing Blvd, Indianapolis, IN 46240, USA
    ##   Unnamed Road, Indianapolis, IN 46240, USA
    ##   Indianapolis, IN 46240, USA
    ##   Washington Township, Indianapolis, IN, USA
    ##   Washington Township, IN, USA
    ##   Indianapolis, IN, USA
    ##   Marion County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.73210144,-104.9554977&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1045 Clayton St, Denver, CO 80206, USA
    ##   1001 Clayton St, Denver, CO 80206, USA
    ##   2774 E 10th Ave, Denver, CO 80206, USA
    ##   2799-2775 E 10th Ave, Denver, CO 80206, USA
    ##   Congress Park, Denver, CO 80206, USA
    ##   Denver, CO 80206, USA
    ##   Denver, CO, USA
    ##   Denver County, Denver, CO, USA
    ##   Colorado, USA
    ##   Rocky Mountains
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=47.42410278,-122.574501&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   13585 Fagerud Rd SE, Olalla, WA 98359, USA
    ##   13603 Fagerud Rd SE, Olalla, WA 98359, USA
    ##   6242 Agape Ct SE, Olalla, WA 98359, USA
    ##   Olalla, WA 98359, USA
    ##   Kitsap County, WA, USA
    ##   Washington, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=31.49090576,74.36810303&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Madina Colony, Lahore, Punjab, Pakistan
    ##   Madina Colony, Lahore, Punjab, Pakistan
    ##   Lahore Cantt, Lahore, Punjab, Pakistan
    ##   Lahore, Punjab, Pakistan
    ##   Punjab, Pakistan
    ##   Pakistan
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.67340088,-87.50980377&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1701 Wabash Ave, Vincennes, IN 47591, USA
    ##   1714 Wabash Ave, Vincennes, IN 47591, USA
    ##   1705 Wabash Ave, Vincennes, IN 47591, USA
    ##   1601-1699 Wabash Ave, Vincennes, IN 47591, USA
    ##   Vincennes, IN 47591, USA
    ##   Vincennes Township, IN 47591, USA
    ##   Knox County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=48.85820007,2.338699341&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   79 Quai des Tuileries, 75001 Paris, France
    ##   ask köprüsü, Pont des Arts, 75001 Paris, France
    ##   Pont des Arts, 75001 Paris, France
    ##   1st arrondissement of Paris, 75001 Paris, France
    ##   75001 Paris, France
    ##   Saint-Germain-l'Auxerrois, Paris, France
    ##   Paris, France
    ##   Île-de-France, France
    ##   France
    ## Multiple addresses found, the first will be returned:
    ##   62 Strathallan Rd, Macleod VIC 3085, Australia
    ##   60 Strathallan Rd, Macleod VIC 3085, Australia
    ##   59 Strathallan Rd, Macleod VIC 3085, Australia
    ##   64-62 Strathallan Rd, Macleod VIC 3085, Australia
    ##   Macleod VIC 3085, Australia
    ##   Macleod West VIC 3085, Australia
    ##   Banyule, VIC, Australia
    ##   Melbourne VIC, Australia
    ##   Victoria, Australia
    ##   Australia
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-37.57569885,144.7193909&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   2-10 Anderson Rd, Sunbury VIC 3429, Australia
    ##   35 Cornish St, Sunbury VIC 3429, Australia
    ##   3 Anderson Rd, Sunbury VIC 3429, Australia
    ##   22-2 Anderson Rd, Sunbury VIC 3429, Australia
    ##   Sunbury VIC 3429, Australia
    ##   Wildwood VIC 3429, Australia
    ##   Hume, VIC, Australia
    ##   Victoria, Australia
    ##   Australia
    ## Multiple addresses found, the first will be returned:
    ##   The Leather Bottle PH, Hemel Hempstead HP2 4PZ, UK
    ##   109 Leverstock Green Way, Hemel Hempstead HP3 8QE, UK
    ##   109 A4147, Hemel Hempstead HP3 8QE, UK
    ##   A4147, Hemel Hempstead HP3 8QE, UK
    ##   Hemel Hempstead HP2 4PZ, UK
    ##   Hemel Hempstead, UK
    ##   Hemel Hempstead HP3, UK
    ##   Dacorum District, UK
    ##   Hertfordshire, UK
    ##   England, UK
    ##   Great Britain, United Kingdom
    ##   United Kingdom
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=43.604599,1.445098877&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Charles de Gaulle Square, 8 Rue du Poids de l'Huile, 31000 Toulouse, France
    ##   Capitole, 31000 Toulouse, France
    ##   19 Rue Lafayette, 31000 Toulouse, France
    ##   Rue Lafayette, 31000 Toulouse, France
    ##   Capitole de Toulouse, Toulouse, France
    ##   31000 Toulouse, France
    ##   Toulouse, France
    ##   Haute-Garonne, France
    ##   Occitanie, France
    ##   France
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=8.48550415,76.94918823&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Sivakami Building, East Fort, Chalai Bazaar, Chalai, Thiruvananthapuram, Kerala 695036, India
    ##   Thakaraparambu Flyover, East Fort, Chalai Bazaar, Chalai, Thiruvananthapuram, Kerala 695001, India
    ##   Chalai Bazaar, Chalai, Thiruvananthapuram, Kerala, India
    ##   Chalai, Thiruvananthapuram, Kerala, India
    ##   Thiruvananthapuram, Kerala 695036, India
    ##   East Fort, Pavithra Nagar, East Fort, Pazhavangadi, Thiruvananthapuram, Kerala, India
    ##   Thiruvananthapuram, Kerala, India
    ##   Kerala, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=44.30900574,8.477203369&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Piazza del Popolo, 40R, 17100 Savona SV, Italy
    ##   Savona - piazza mameli, 17100 Savona SV, Italy
    ##   Piazza del Popolo, 5, 17100 Savona SV, Italy
    ##   Piazza del Popolo, 52, 17100 Savona SV, Italy
    ##   17100 Savona, Province of Savona, Italy
    ##   Province of Savona, Italy
    ##   Liguria, Italy
    ##   Italy
    ## Multiple addresses found, the first will be returned:
    ##   8571 Woodland Green Ct, Cordova, TN 38016, USA
    ##   8594 Woodland Green Ct, Cordova, TN 38016, USA
    ##   Cordova Rd, Cordova, TN 38016, USA
    ##   Cordova, TN 38016, USA
    ##   Cordova, Memphis, TN, USA
    ##   Memphis, TN, USA
    ##   Shelby County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   140 Morganza Rd, Canonsburg, PA 15317, USA
    ##   400 Southpointe Blvd, Canonsburg, PA 15317, USA
    ##   Morganza Rd, Canonsburg, PA 15317, USA
    ##   North Strabane Township, PA, USA
    ##   Canonsburg, PA 15317, USA
    ##   Washington County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.32229614,-74.60079956&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   414 7th St, Somers Point, NJ 08244, USA
    ##   425 7th St, Somers Point, NJ 08244, USA
    ##   550 New Rd, Somers Point, NJ 08244, USA
    ##   470 7th St, Somers Point, NJ 08244, USA
    ##   Somers Point, NJ, USA
    ##   Somers Point, NJ 08244, USA
    ##   Atlantic County, NJ, USA
    ##   New Jersey, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.85740662,-77.09999847&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1301 S George Mason Dr, Arlington, VA 22204, USA
    ##   S George Mason Drive, SB @ 12th Road S, NS, Arlington, VA 22204, USA
    ##   1233 S George Mason Dr, Arlington, VA 22204, USA
    ##   S George Mason Dr, Arlington, VA 22204, USA
    ##   Douglas Park, Arlington, VA 22204, USA
    ##   Arlington, VA 22204, USA
    ##   Arlington County, Arlington, VA, USA
    ##   Arlington, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=39.13609314,-77.28240204&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   14 Indian Grass Ct, Germantown, MD 20874, USA
    ##   13628 Monarch Vista Dr, Germantown, MD 20874, USA
    ##   17019 Indian Grass Dr, Germantown, MD 20874, USA
    ##   17108-17100 Indian Grass Dr, Germantown, MD 20874, USA
    ##   Germantown, MD 20874, USA
    ##   6, MD, USA
    ##   Montgomery County, MD, USA
    ##   Maryland, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   20/404B, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   41, Thambu Swamy Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Manonmani Ammal Rd, Kilpauk, Chennai, Tamil Nadu 600010, India
    ##   Kilpauk, Chennai, Tamil Nadu, India
    ##   Chennai, Tamil Nadu 600010, India
    ##   Chennai, Tamil Nadu, India
    ##   Tamil Nadu, India
    ##   India
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.10049438,-75.37090302&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   146 Crossfield Rd, King of Prussia, PA 19406, USA
    ##   Upper Merion Township Park, 175 W Valley Forge Rd, King of Prussia, PA 19406, USA
    ##   139 Crossfield Rd, King of Prussia, PA 19406, USA
    ##   114-134 Crossfield Rd, King of Prussia, PA 19406, USA
    ##   King of Prussia, PA, USA
    ##   KNG OF PRUSSA, PA 19406, USA
    ##   Upper Merion Township, PA, USA
    ##   Montgomery County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=-27.47160339,153.0213928&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   100B N Quay, Brisbane City QLD 4000, Australia
    ##   Pacific Mwy, Brisbane City QLD 4000, Australia
    ##   Brisbane City QLD 4000, Australia
    ##   Petrie Terrace QLD 4000, Australia
    ##   Brisbane, QLD, Australia
    ##   Brisbane QLD, Australia
    ##   Queensland, Australia
    ##   Australia
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=41.76890564,-71.47579956&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   15 Meshanticut Dr, Cranston, RI 02920, USA
    ##   19 Lake View Rd, Cranston, RI 02920, USA
    ##   93 Dean St, Cranston, RI 02920, USA
    ##   160 Lakeview Rd, Cranston, RI 02920, USA
    ##   Cranston, RI 02920, USA
    ##   Cranston, RI, USA
    ##   Providence County, RI, USA
    ##   Rhode Island, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, Exeter, NH 03833, USA
    ##   Exeter, NH 03833, USA
    ##   Kensington, NH 03833, USA
    ##   Rockingham County, NH, USA
    ##   New Hampshire, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.56289673,-112.0519028&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   8603 N 14th St, Phoenix, AZ 85020, USA
    ##   8607 N 14th St, Phoenix, AZ 85020, USA
    ##   8614 N 14th St, Phoenix, AZ 85020, USA
    ##   8748-8722 N 14th St, Phoenix, AZ 85020, USA
    ##   Phoenix, AZ 85020, USA
    ##   North Mountain Village, Phoenix, AZ, USA
    ##   Phoenix, AZ, USA
    ##   Maricopa County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=42.47180176,-96.35489655&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   4005 Morningside Ave, Sioux City, IA 51106, USA
    ##   1818 S St Aubin St, Sioux City, IA 51106, USA
    ##   4105 Morningside Ave, Sioux City, IA 51106, USA
    ##   4050 Orleans Ave, Sioux City, IA 51106, USA
    ##   4199-4099 Orleans Ave, Sioux City, IA 51106, USA
    ##   Sioux City, IA 51106, USA
    ##   Sioux City, IA, USA
    ##   Woodbury County, IA, USA
    ##   Iowa, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.32659912,-84.19280243&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1020 Main St, Jacksboro, TN 37757, USA
    ##   1062 Main St, Jacksboro, TN 37757, USA
    ##   1016 Main St, Jacksboro, TN 37757, USA
    ##   1022 Main St, Jacksboro, TN 37757, USA
    ##   Appalachian Hwy, Jacksboro, TN 37757, USA
    ##   Jacksboro, TN 37757, USA
    ##   Campbell County, TN, USA
    ##   Tennessee, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=30.84939575,-86.20230103&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Price Rd, Defuniak Springs, FL 32433, USA
    ##   1015 McKee Rd, Defuniak Springs, FL 32433, USA
    ##   Defuniak Springs, FL 32433, USA
    ##   Walton County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=34.70550537,-112.2639008&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   11425 E Mingus Vista Dr, Prescott Valley, AZ 86315, USA
    ##   N Prescott Ridge Rd, Prescott Valley, AZ 86315, USA
    ##   Prescott Valley, AZ 86315, USA
    ##   Yavapai County, AZ, USA
    ##   Arizona, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.09440613,-95.97170258&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Hawthorne Park, 4670 S Rockford Ave, Tulsa, OK 74105, USA
    ##   4670 S Rockford Ave, Tulsa, OK 74105, USA
    ##   4674 S Rockford Ave, Tulsa, OK 74105, USA
    ##   4600-4798 S Quincy Pl, Tulsa, OK 74105, USA
    ##   Tulsa, OK 74105, USA
    ##   Tulsa, OK, USA
    ##   Tulsa County, OK, USA
    ##   Oklahoma, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.84759521,-77.32810211&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   11000 Berry St, Fairfax, VA 22030, USA
    ##   11014 Byrd Dr, Fairfax, VA 22030, USA
    ##   11016 Byrd Dr, Fairfax, VA 22030, USA
    ##   10974-11098 Berry St, Fairfax, VA 22030, USA
    ##   Fairfax, VA, USA
    ##   Fairfax, VA 22030, USA
    ##   Virginia, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=36.93649292,-84.09010315&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   1405 S Main St, Corbin, KY 40701, USA
    ##   1401 S Main St, Corbin, KY 40701, USA
    ##   1403 Hwy 25, Corbin, KY 40701, USA
    ##   199-101 W 15th St, Corbin, KY 40701, USA
    ##   Corbin, KY 40701, USA
    ##   Whitley County, KY, USA
    ##   Kentucky, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=45.28250122,-93.41860199&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   17149 Potassium St NW, Ramsey, MN 55303, USA
    ##   17201 St Francis Blvd NW, Ramsey, MN 55303, USA
    ##   17164 Potassium St NW, Ramsey, MN 55303, USA
    ##   17164-17156 St Francis Blvd NW, Ramsey, MN 55303, USA
    ##   Ramsey, MN 55303, USA
    ##   Oak Grove, MN 55303, USA
    ##   Anoka County, MN, USA
    ##   Minnesota, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.30610657,-75.14830017&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   PA-611, Doylestown, PA 18901, USA
    ##   Doylestown Township, PA, USA
    ##   New Britain, PA 18901, USA
    ##   Bucks County, PA, USA
    ##   Pennsylvania, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.46380615,-77.39800262&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   7370 Wilton Rd, Richmond, VA 23231, USA
    ##   7336 Osborne Turnpike, Henrico, VA 23231, USA
    ##   7382 Osborne Turnpike, Henrico, VA 23231, USA
    ##   7505-7501 Wilton Rd, Henrico, VA 23231, USA
    ##   Richmond, VA 23231, USA
    ##   Varina, VA, USA
    ##   Henrico County, VA, USA
    ##   Virginia, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   4413 SW 129th Ave, Miami, FL 33175, USA
    ##   4415 SW 129th Ave, Miami, FL 33175, USA
    ##   SW 44th Terrace, Miami, FL 33175, USA
    ##   Miami, FL 33175, USA
    ##   Kendale Lakes, FL, USA
    ##   Miami-Dade County, FL, USA
    ##   Florida, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=37.38340759,-5.978897095&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Unnamed Road, 41018 Sevilla, Spain
    ##   41018 Seville, Spain
    ##   Nervión, Seville, Spain
    ##   Seville, Spain
    ##   Municipality of Seville, Seville, Spain
    ##   Comarca Metropolitana de Sevilla, Seville, Spain
    ##   Andalusia, Spain
    ##   Spain
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=33.73039246,-116.710701&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   27470 Saunders Meadow Rd, Idyllwild, CA 92549, USA
    ##   2745 Deer Trail, Idyllwild, CA 92549, USA
    ##   Deer Trail, Idyllwild, CA 92549, USA
    ##   Idyllwild-Pine Cove, CA, USA
    ##   Idyllwild, CA 92549, USA
    ##   Riverside County, CA, USA
    ##   California, USA
    ##   United States
    ## Multiple addresses found, the first will be returned:
    ##   1/A, Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka 560001, India
    ##   Unnamed Road, Ambedkar Veedhi, Bengaluru, Karnataka 560001, India
    ##   Ambedkar Veedhi, Sampangi Rama Nagar, Bengaluru, Karnataka, India
    ##   Bengaluru, Karnataka 560001, India
    ##   Bengaluru, Karnataka, India
    ##   Bangalore Urban, Karnataka, India
    ##   Karnataka, India
    ##   India
    ## Multiple addresses found, the first will be returned:
    ##   1239 S 300 W, Rensselaer, IN 47978, USA
    ##   1556 S County Rd 300 W, Rensselaer, IN 47978, USA
    ##   Unnamed Road, Collegeville, IN 47978, USA
    ##   Barkley Township, IN, USA
    ##   Rensselaer, IN 47978, USA
    ##   Jasper County, IN, USA
    ##   Indiana, USA
    ##   United States
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=40.75689697,29.81469727&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   Sirripasa, Çavdar Cd. No:2, 41900 Derince/Kocaeli, Turkey
    ##   Sirripasa, Denizciler Cd. 218-236, 41900 Derince/Kocaeli, Turkey
    ##   Sirripasa, 41900 Derince/Kocaeli, Turkey
    ##   Derince, Kocaeli, Turkey
    ##   Derince/Kocaeli, Turkey
    ##   Kocaeli, Turkey
    ##   Turkey
    ## Source : https://maps.googleapis.com/maps/api/geocode/json?latlng=38.959198,-94.59609985&key=xxx-pEUMlBXWdlDdYvh0t2B473OUbas
    ## Multiple addresses found, the first will be returned:
    ##   On Wornall at S Ward Pkwy Southbound, Kansas City, MO 64114, USA
    ##   9237 Ward Pkwy, Kansas City, MO 64114, USA
    ##   8237 Ward Parkway Median Crossing, Kansas City, MO 64114, USA
    ##   9243 Ward Pkwy, Kansas City, MO 64114, USA
    ##   Ward Pkwy, Kansas City, MO 64114, USA
    ##   Ward Parkway Estates, Kansas City, MO 64114, USA
    ##   Kansas City, MO 64114, USA
    ##   Kaw Township, MO, USA
    ##   Kansas City, MO, USA
    ##   Jackson County, MO, USA
    ##   Missouri, USA
    ##   United States

``` r
# based on geo information, it looks like we have 6 possible duplicate entries
d[duplicated(d)]
```

    ##    study.num duration      lat     long screentime work.phone
    ## 1:         2       26 13.08459 80.24841        Yes        Yes
    ## 2:         2       26 13.08459 80.24841        Yes        Yes
    ## 3:         2       26 13.08459 80.24841        Yes        Yes
    ## 4:         2       36 13.08459 80.24841        Yes        Yes
    ## 5:         2       11 13.08459 80.24841        Yes        Yes
    ## 6:         2       11 13.08459 80.24841        Yes        Yes
    ##                          phone.provided gender age employment.status
    ## 1: Yes, including cellular network fees Female  24         Full time
    ## 2: Yes, including cellular network fees Female  24         Full time
    ## 3: Yes, including cellular network fees   Male  24         Full time
    ## 4: Yes, including cellular network fees   Male  24         Full time
    ## 5: Yes, including cellular network fees   Male  26         Full time
    ## 6: Yes, including cellular network fees   Male  26         Full time
    ##    employment.type minutes.day minutes.week
    ## 1:     Blue Collar          35            7
    ## 2:     Blue Collar          35            7
    ## 3:     Blue Collar          35            7
    ## 4:     Blue Collar          35            7
    ## 5:     Blue Collar          35          197
    ## 6:     Blue Collar          35          197
    ##                                                                           location
    ## 1: No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ## 2: No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ## 3: No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ## 4: No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ## 5: No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India
    ## 6: No. 41, Mano Mani Ammal Koil Street, Kilpauk, Chennai, Tamil Nadu 600010, India

``` r
# let's remove them for the sake of possible biases
d <- d[!duplicated(d)]
```

``` r
hist(d$age)
```

![](FinalEssay_Anderson_Tucker_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
hist(d$duration)
```

![](FinalEssay_Anderson_Tucker_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

### Conclusion

Despite not being able to conduct a true field experiment, we were able
to gather a large baseline dataset of iOS users with their screentime
and a number of useful covariates.
