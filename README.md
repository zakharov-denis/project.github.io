
<!DOCTYPE html>

<html>

<head>

<meta charset="utf-8" />
<meta name="generator" content="pandoc" />
<meta http-equiv="X-UA-Compatible" content="IE=EDGE" />




<title>Data Cleaning Process</title>

<script src="site_libs/header-attrs-2.16/header-attrs.js"></script>
<script src="site_libs/jquery-3.6.0/jquery-3.6.0.min.js"></script>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<link href="site_libs/bootstrap-3.3.5/css/bootstrap.min.css" rel="stylesheet" />
<script src="site_libs/bootstrap-3.3.5/js/bootstrap.min.js"></script>
<script src="site_libs/bootstrap-3.3.5/shim/html5shiv.min.js"></script>
<script src="site_libs/bootstrap-3.3.5/shim/respond.min.js"></script>
<style>h1 {font-size: 34px;}
       h1.title {font-size: 38px;}
       h2 {font-size: 30px;}
       h3 {font-size: 24px;}
       h4 {font-size: 18px;}
       h5 {font-size: 16px;}
       h6 {font-size: 12px;}
       code {color: inherit; background-color: rgba(0, 0, 0, 0.04);}
       pre:not([class]) { background-color: white }</style>
<script src="site_libs/navigation-1.1/tabsets.js"></script>
<link href="site_libs/highlightjs-9.12.0/default.css" rel="stylesheet" />
<script src="site_libs/highlightjs-9.12.0/highlight.js"></script>

<style type="text/css">
  code{white-space: pre-wrap;}
  span.smallcaps{font-variant: small-caps;}
  span.underline{text-decoration: underline;}
  div.column{display: inline-block; vertical-align: top; width: 50%;}
  div.hanging-indent{margin-left: 1.5em; text-indent: -1.5em;}
  ul.task-list{list-style: none;}
    </style>

<style type="text/css">code{white-space: pre;}</style>
<script type="text/javascript">
if (window.hljs) {
  hljs.configure({languages: []});
  hljs.initHighlightingOnLoad();
  if (document.readyState && document.readyState === "complete") {
    window.setTimeout(function() { hljs.initHighlighting(); }, 0);
  }
}
</script>









<style type = "text/css">
.main-container {
  max-width: 940px;
  margin-left: auto;
  margin-right: auto;
}
img {
  max-width:100%;
}
.tabbed-pane {
  padding-top: 12px;
}
.html-widget {
  margin-bottom: 20px;
}
button.code-folding-btn:focus {
  outline: none;
}
summary {
  display: list-item;
}
details > summary > p:only-child {
  display: inline;
}
pre code {
  padding: 0;
}
</style>


<style type="text/css">
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu>.dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
  border-radius: 0 6px 6px 6px;
}
.dropdown-submenu:hover>.dropdown-menu {
  display: block;
}
.dropdown-submenu>a:after {
  display: block;
  content: " ";
  float: right;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
  border-width: 5px 0 5px 5px;
  border-left-color: #cccccc;
  margin-top: 5px;
  margin-right: -10px;
}
.dropdown-submenu:hover>a:after {
  border-left-color: #adb5bd;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left>.dropdown-menu {
  left: -100%;
  margin-left: 10px;
  border-radius: 6px 0 6px 6px;
}
</style>

<script type="text/javascript">
// manage active state of menu based on current page
$(document).ready(function () {
  // active menu anchor
  href = window.location.pathname
  href = href.substr(href.lastIndexOf('/') + 1)
  if (href === "")
    href = "index.html";
  var menuAnchor = $('a[href="' + href + '"]');

  // mark the anchor link active (and if it's in a dropdown, also mark that active)
  var dropdown = menuAnchor.closest('li.dropdown');
  if (window.bootstrap) { // Bootstrap 4+
    menuAnchor.addClass('active');
    dropdown.find('> .dropdown-toggle').addClass('active');
  } else { // Bootstrap 3
    menuAnchor.parent().addClass('active');
    dropdown.addClass('active');
  }

  // Navbar adjustments
  var navHeight = $(".navbar").first().height() + 15;
  var style = document.createElement('style');
  var pt = "padding-top: " + navHeight + "px; ";
  var mt = "margin-top: -" + navHeight + "px; ";
  var css = "";
  // offset scroll position for anchor links (for fixed navbar)
  for (var i = 1; i <= 6; i++) {
    css += ".section h" + i + "{ " + pt + mt + "}\n";
  }
  style.innerHTML = "body {" + pt + "padding-bottom: 40px; }\n" + css;
  document.head.appendChild(style);
});
</script>

<!-- tabsets -->

<style type="text/css">
.tabset-dropdown > .nav-tabs {
  display: inline-table;
  max-height: 500px;
  min-height: 44px;
  overflow-y: auto;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.tabset-dropdown > .nav-tabs > li.active:before {
  content: "";
  font-family: 'Glyphicons Halflings';
  display: inline-block;
  padding: 10px;
  border-right: 1px solid #ddd;
}

.tabset-dropdown > .nav-tabs.nav-tabs-open > li.active:before {
  content: "&#xe258;";
  border: none;
}

.tabset-dropdown > .nav-tabs.nav-tabs-open:before {
  content: "";
  font-family: 'Glyphicons Halflings';
  display: inline-block;
  padding: 10px;
  border-right: 1px solid #ddd;
}

.tabset-dropdown > .nav-tabs > li.active {
  display: block;
}

.tabset-dropdown > .nav-tabs > li > a,
.tabset-dropdown > .nav-tabs > li > a:focus,
.tabset-dropdown > .nav-tabs > li > a:hover {
  border: none;
  display: inline-block;
  border-radius: 4px;
  background-color: transparent;
}

.tabset-dropdown > .nav-tabs.nav-tabs-open > li {
  display: block;
  float: none;
}

.tabset-dropdown > .nav-tabs > li {
  display: none;
}
</style>

<!-- code folding -->




</head>

<body>


<div class="container-fluid main-container">




<div class="navbar navbar-default  navbar-fixed-top" role="navigation">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-bs-toggle="collapse" data-target="#navbar" data-bs-target="#navbar">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="index.html">Cyclistic Case Study</a>
    </div>
    <div id="navbar" class="navbar-collapse collapse">
      <ul class="nav navbar-nav">
        <li>
  <a href="index.html">Home</a>
</li>
<li>
  <a href="Data-Cleaning-Process.html">Data Cleaning Process</a>
</li>
<li>
  <a href="Data-Analysis---Visualization.html">Data Analysis</a>
</li>
<li>
  <a href="Final-Report.html">Final Report</a>
</li>
      </ul>
      <ul class="nav navbar-nav navbar-right">
        
      </ul>
    </div><!--/.nav-collapse -->
  </div><!--/.container -->
</div><!--/.navbar -->

<div id="header">



<h1 class="title toc-ignore">Data Cleaning Process</h1>

</div>


<p><br />
<br />
</p>
<div id="document-description" class="section level3">
<h3>1. Document Description</h3>
<hr />
<p>This document describes all the steps taken to clean and transform
Cyclistic’s raw datasets to prepare the data for the analysis stage. For
the purpose of this case study, the data has been collected for the
months of August 2021 to July 2022. The dataset can be downloaded <a
href="https://divvy-tripdata.s3.amazonaws.com/index.html">here</a>.<br />
<br />
Please note that Cyclistic is a fictional company. Raw data has been
collected by Motivate International Inc. the company which operates the
City of Chicago’s Divvy bicycle sharing service. The license to use this
public dataset can be found <a
href="https://ride.divvybikes.com/data-license-agreement">here</a>.<br />
<br />
These were some of the packages used for the data cleaning process.</p>
<pre class="r"><code>library(tidyverse)
library(lubridate)
library(stringr)
library(scales)</code></pre>
<p><br />
<br />
<br />
</p>
</div>
<div id="combine-datasets" class="section level3">
<h3>2. Combine Datasets</h3>
<hr />
<p><strong>2.1 Load Raw Data</strong></p>
<p>We will create separate dataframes for loading data from August 2021
to July 2022.</p>
<pre class="r"><code>trip_202108 &lt;- read_csv(&quot;202108-divvy-tripdata/202108.csv&quot;)
trip_202109 &lt;- read_csv(&quot;202109-divvy-tripdata/202109.csv&quot;)
trip_202110 &lt;- read_csv(&quot;202110-divvy-tripdata/202110.csv&quot;)
trip_202111 &lt;- read_csv(&quot;202111-divvy-tripdata/202111.csv&quot;)
trip_202112 &lt;- read_csv(&quot;202112-divvy-tripdata/202112.csv&quot;)
trip_202201 &lt;- read_csv(&quot;202201-divvy-tripdata/202201.csv&quot;)
trip_202202 &lt;- read_csv(&quot;202202-divvy-tripdata/202202.csv&quot;)
trip_202203 &lt;- read_csv(&quot;202203-divvy-tripdata/202203.csv&quot;)
trip_202204 &lt;- read_csv(&quot;202204-divvy-tripdata/202204.csv&quot;)
trip_202205 &lt;- read_csv(&quot;202205-divvy-tripdata/202205.csv&quot;)
trip_202206 &lt;- read_csv(&quot;202206-divvy-tripdata/202206.csv&quot;)
trip_202207 &lt;- read_csv(&quot;202207-divvy-tripdata/202207.csv&quot;)</code></pre>
<p><br />
<strong>2.2 Check for data structure</strong></p>
<p>The structure summary outputs will help us identify if any of the
individual datasets have different string types, column names etc.</p>
<pre class="r"><code>str(trip_202108)
str(trip_202109)
str(trip_202110)
str(trip_202111)
str(trip_202112)
str(trip_202201)
str(trip_202202)
str(trip_202203)
str(trip_202204)
str(trip_202205)
str(trip_202206)
str(trip_202207)</code></pre>
<p><br />
We found that all the column names were fine and the string types were
adhering to the data.</p>
<p><br />
</p>
<p><strong>2.3 Merge Datasets</strong></p>
<p>We will merge all 12 datasets into 1 dataframe.</p>
<pre class="r"><code># Combine into a single DataFrame

all_trips &lt;- bind_rows(trip_202108, trip_202109, trip_202110, trip_202111, trip_202112,
                       trip_202201, trip_202202, trip_202203, trip_202204, trip_202205,
                       trip_202206, trip_202207)</code></pre>
<p><br />
<br />
<br />
</p>
</div>
<div id="prepare-dataset" class="section level3">
<h3>3. Prepare Dataset</h3>
<hr />
<p><strong>3.1 Calculating Ride Length</strong></p>
<p>Ride length will help us in further analysis and would also let us
know if there are any rides less than 0.</p>
<pre class="r"><code># Calculating trip time in secs

all_trips &lt;- mutate(all_trips, trip_time = ended_at - started_at)

# Converting trip time to numeric data type

all_trips$trip_time &lt;- as.numeric(as.character(all_trips$trip_time))</code></pre>
<p><br />
<strong>3.2 Summarise by date variables</strong></p>
<p>We will add separate columns for date variables (date, month, day of
week, week, time of day etc.) which will help us in future analysis.</p>
<pre class="r"><code># Date

all_trips &lt;- all_trips %&gt;% 
  mutate(Date = as.Date(started_at))

# Day of week

all_trips &lt;- all_trips %&gt;% 
  mutate(day_of_week = wday(all_trips$started_at, label=TRUE))

# Month

all_trips &lt;- all_trips %&gt;% 
  mutate(month_name = format(started_at, &quot;%m&quot;))
         
# Year

all_trips &lt;- all_trips %&gt;% 
  mutate(year = year(ymd(Date)))
         
# Day

all_trips &lt;- all_trips %&gt;% 
  mutate(day= day(ymd(Date)))

# Time of Day

all_trips &lt;- all_trips %&gt;% 
  mutate(Time_of_Day = format(as.POSIXct(started_at), format = &quot;%H:%M:%S&quot;))</code></pre>
<p><br />
<br />
<br />
</p>
</div>
<div id="clean-the-dataset" class="section level3">
<h3>4. Clean the dataset</h3>
<hr />
<p><strong>4.1 Remove rows with ride length &lt; 0</strong></p>
<p>As identified in section 3.1, there were some rows with ride length
less than 0. These rides were those where Divvy took bikes out of
circulation for Quality Control reasons. We will want to delete these
rides.</p>
<pre class="r"><code># Creating a separate dataframe for trip time greater than 0

all_trips_v2 &lt;- all_trips_v2 %&gt;% 
  filter(trip_time&gt;0) 

# Sorting dataset by starting time

all_trips_v2 &lt;- arrange(all_trips_v2, started_at)</code></pre>
<p><br />
<strong>4.2 Remove rows with incomplete data</strong></p>
<p>There were some instances where the station names were not recorded.
We can check and remove these stations from our dataset.</p>
<pre class="r"><code># Remove blank or NA rows from start station name and end station name

## We will use this dataframe for further analysis

trips_cleaned &lt;- all_trips %&gt;% 
  filter(!is.na(start_station_name) | start_station_name==&quot;&quot;) %&gt;% 
  filter(!is.na(end_station_name) | end_station_name==&quot;&quot;)</code></pre>
<p><br />
<strong>4.3 Checking for Inconsistencies</strong></p>
<p>We will check for inconsistencies in the start and end station names
and if all the stations are in title case.</p>
<pre class="r"><code>#Check for inconsistencies in start station names

trips_cleaned %&gt;%
  filter(
    str_detect(start_station_name, &quot;[:upper:]&quot;)
    &amp; !str_detect(start_station_name,&quot;[:lower:]&quot;)
  ) %&gt;%
  
  group_by(
    start_station_name
  ) %&gt;%
  
  count(
    start_station_name
  )

#Check for inconsistencies in end station names

trips_cleaned %&gt;%
  filter(
    str_detect(end_station_name, &quot;[:upper:]&quot;)
    &amp; !str_detect(end_station_name,&quot;[:lower:]&quot;)
  ) %&gt;%
  
  group_by(
    end_station_name
  ) %&gt;%
  
  count(
    end_station_name
  )</code></pre>
<p><br />
<strong>4.4 Remove Inconsistencies</strong></p>
<p>We found that there are some station names where the partial name is
either upper or lower. We will change all the station names to title
case.</p>
<pre class="r"><code>#Convert upper and lower station names to title case

trips_cleaned$start_station_name &lt;- str_to_title(trips_cleaned$start_station_name)
trips_cleaned$end_station_name &lt;- str_to_title(trips_cleaned$end_station_name)</code></pre>
<p><br />
<strong>4.5 Checking for duplicates</strong></p>
<p>The ride id is column is unique to each ride. We could use it to
check for any duplicate rows.</p>
<pre class="r"><code>#Checking for duplicate rows

duplicate_check &lt;- trips_cleaned %&gt;%
  count(ride_id) %&gt;%
  filter(n &gt; 1)</code></pre>
<p>There were no duplicate rows observed in the dataset.</p>
<p><br />
<br />
<br />
</p>
</div>
<div id="understand-dataset" class="section level3">
<h3>5. Understand Dataset</h3>
<hr />
<p><strong>5.1 Check rideable type</strong></p>
<pre class="r"><code>#Checking for unique ride types available

unique(trips_cleaned[c(&quot;rideable_type&quot;)])</code></pre>
<p>The above code returned three distinct ride types which are used in
the cleaned dataset. It was done to identify whether a ride type was
added to the dataset at a later date.</p>
<pre class="r"><code>#Creating a separate dataframe to check if any ride type was added after the other

ride_type_added &lt;- trips_cleaned %&gt;% 
  group_by(rideable_type, year, month) %&gt;% 
  count(rideable_type)</code></pre>
<p>We found that all the ride types were added from the starting i.e Aug
2021 from the dataset.</p>
<p><br />
</p>
<p><strong>5.2 Check station names</strong></p>
<p>There might be some instances where some stations might be added or
removed from Cyclistic’s Portfolio. This can be reviewed using below
code:<br />
Firstly a dataframe which lists unique station names should be
created.</p>
<pre class="r"><code>#Identify unique station names

unique_station_names &lt;- trips_cleaned %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) </code></pre>
<p>Further the dataframes which lists the unique station names used each
month should be created</p>
<pre class="r"><code>#Aug 2021 dataframe which lists the unique station names used each month

Aug_21 &lt;- trips_cleaned %&gt;% 
  filter(year==2021 &amp; month==8) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Sep 2021 dataframe which lists the unique station names used each month

Sep_21 &lt;- trips_cleaned %&gt;% 
  filter(year==2021 &amp; month==9) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Oct 2021 dataframe which lists the unique station names used each month

Oct_21 &lt;- trips_cleaned %&gt;% 
  filter(year==2021 &amp; month==10) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Nov 2021 dataframe which lists the unique station names used each month

Nov_21 &lt;- trips_cleaned %&gt;% 
  filter(year==2021 &amp; month==11) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Dec 2021 dataframe which lists the unique station names used each month

Dec_21 &lt;- trips_cleaned %&gt;% 
  filter(year==2021 &amp; month==12) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Jan 2022 dataframe which lists the unique station names used each month

Jan_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==1) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Feb 2022 dataframe which lists the unique station names used each month

Feb_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==2) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Mar 2022 dataframe which lists the unique station names used each month

Mar_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==3) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Apr 2022 dataframe which lists the unique station names used each month

Apr_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==4) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#May 2022 dataframe which lists the unique station names used each month

May_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==5) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 

#Jun 2022 dataframe which lists the unique station names used each month  

Jun_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==6) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) 
  
#Jul 2022 dataframe which lists the unique station names used each month

Jul_22 &lt;- trips_cleaned %&gt;% 
  filter(year==2022 &amp; month==7) %&gt;% 
  group_by(start_station_name) %&gt;% 
  count(start_station_name) </code></pre>
<p>Each unique station name can be tested against the monthly filter
data frames to assess which unique station name was used in a particular
month.</p>
<pre class="r"><code>#Checking whether station is being used in particular month

unique_station_names$Aug_21 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Aug_21$start_station_name)

unique_station_names$Sep_21 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Sep_21$start_station_name)

unique_station_names$Oct_21 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Oct_21$start_station_name)

unique_station_names$Nov_21 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Nov_21$start_station_name)

unique_station_names$Dec_21 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Dec_21$start_station_name)

unique_station_names$Jan_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Jan_22$start_station_name)

unique_station_names$Feb_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Feb_22$start_station_name)

unique_station_names$Mar_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Mar_22$start_station_name)

unique_station_names$Apr_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Apr_22$start_station_name)

unique_station_names$May_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% May_22$start_station_name)

unique_station_names$Jun_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Jun_22$start_station_name)

unique_station_names$Jul_22 &lt;- as.integer(unique_station_names$start_station_name
                                          %in% Jul_22$start_station_name)

#Adding column for count of occurences for all the months

unique_station_names$count &lt;- rowSums(unique_station_names[,3:14])</code></pre>
<p>We will check which stations were added or removed in the Cyclistic
POrtfolio in this particular time. For this purpose two months were used
in each filter in order to avoid any anomalies whereby a station was
simply not used for the month instead of the station being completely
removed or added to Cyclistic’s portfolio.<br />
FOr analyzing stations added, we will find the count of occurence of
each station for the August 21 and September 21 less than 1. Similarly,
we will find it for June 22 and July 22 less than 1 for finding the
stations removed.</p>
<pre class="r"><code>#Checking whether the station is recently added in the rider&#39;s portfolio 

station_check_A &lt;- unique_station_names %&gt;% 
  filter(Aug_21&lt;1 &amp; Sep_21&lt;1) 

#Checking whether the station is recently deleted from the portfolio

station_check_B &lt;- unique_station_names %&gt;% 
  filter(Jun_22&lt;1 &amp; Jul_22&lt;1)</code></pre>
<p>This showed us that out of 1306 unique station names 546 stations
were added and 39 stations were removed from the cyclistic Portfolio
during the analysis period.</p>
<p><br />
</p>
<p><strong>5.3 Checking for distinct member types</strong></p>
<p>Let’s check the distinct type of members in the dataset. From the
data given we know that there are two categories of riders : member
&amp; casual</p>
<pre class="r"><code>unique(trips_cleaned[c(&quot;member_casual&quot;)])</code></pre>
<p><br />
<br />
<br />
</p>
</div>
<div id="save-the-dataset" class="section level3">
<h3>6. Save the Dataset</h3>
<hr />
<p>Finally, we will save the cleaned dataset for further analysis.</p>
<pre class="r"><code>#Save the cleaned dataset

write.csv(trips_cleaned, file = &quot;C:/Users/jains/Downloads/Cyclistic Project/Trip_Data_082021-072022/Cyclistic_Combined_Data.csv&quot;)

#Save additional useful datasets

write.csv(all_trips, file = &quot;C:/Users/jains/Downloads/Cyclistic Project/Trip_Data_082021-072022/all_trips.csv&quot;)

write.csv(ride_type_added, file = &quot;C:/Users/jains/Downloads/Cyclistic Project/Trip_Data_082021-072022/ride_type_check.csv&quot;)

write.csv(unique_station_names, file = &quot;C:/Users/jains/Downloads/Cyclistic Project/Trip_Data_082021-072022/station_name_check.csv&quot;)</code></pre>
</div>




</div>

<script>

// add bootstrap table styles to pandoc tables
function bootstrapStylePandocTables() {
  $('tr.odd').parent('tbody').parent('table').addClass('table table-condensed');
}
$(document).ready(function () {
  bootstrapStylePandocTables();
});


</script>

<!-- tabsets -->

<script>
$(document).ready(function () {
  window.buildTabsets("TOC");
});

$(document).ready(function () {
  $('.tabset-dropdown > .nav-tabs > li').click(function () {
    $(this).parent().toggleClass('nav-tabs-open');
  });
});
</script>

<!-- code folding -->


<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src  = "https://mathjax.rstudio.com/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML";
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>

</body>
</html>

