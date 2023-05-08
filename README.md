Download Link: https://assignmentchef.com/product/solved-purple-america
<br>
Write a program to visualize U.S. presidential election results.

<b>Historical context.</b> During coverage of the 2000 presidential election, Tim Russert coined the political terms <em>red states</em> and <em>blue states</em> to refer to states that predominantly vote for the Republican presidential candidate (red) or the Democratic presidential candidate (blue). The news media use red-state blue-state maps, such as the one below, to display election results.

<blockquote>

 <blockquote>

  <img decoding="async" alt="Tim Russert, red-states, blue-states" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/russert.png?w=980" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

   <noscript>

    <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/russert.png?w=980" alt="Tim Russert, red-states, blue-states" data-recalc-dims="1">

   </noscript>

 </blockquote>

</blockquote>

<b>The problem.</b> On this assignment, you will create more refined (and less polarizing) <em>choropleth maps</em> by mashing up two sources of data: geographic boundary data and election return data.

<b>Geographic data.</b> We supply geographic data (sourced from the <a href="https://www.census.gov/tiger/boundary">U.S. Census</a>) that describes the boundary of each state and county in the United States.

<ul>

 <li>The first line consists of four real numbers, representing the bounding box of the region. The first two numbers are the minimum longitude and latitude values; the second two numbers are the maximum longitude and latitude values.</li>

 <li>The next line is an integer that specifies the number of subregions.</li>

 <li>There is one block for each subregion (with a blank line separates blocks):

  <ul>

   <li>The first line of a block is an integer <em>N</em> that specifies the number of points in the polygon describing the subregion.</li>

   <li>The second line of a block is a string that is the name of the subregion.</li>

   <li>The third line of a block is a string that is the name of the region.</li>

   <li>The remaining <em>N</em> lines of the block describe the polygonal boundary, given as <em>N</em> pairs of real numbers, representing the longitude and latitude coordinates.</li>

  </ul></li>

</ul>

<table border="0" cellspacing="0" cellpadding="0" bgcolor="#FFFFFF">

 <tbody>

  <tr>

   <td valign="top">

    <blockquote>

     <pre>% <b>more <a href="http://nifty.stanford.edu/2014/wayne-purple-america/data/USA.txt">USA.txt</a>                    </b>-124.731216   24.544102 -66.980385   49.384365104AlabamaUSA498 -88.200027   34.995548 -88.202919   35.007942 -87.984886   35.005848... -88.153519   34.921185 -88.176064   34.962433 -88.187088   34.974182...WyomingUSA68-111.048203   44.474144-111.054558   44.666336-111.054420   45.001392  ...-111.043846   43.315800-111.044724   43.501213-111.046272   43.983456</pre>

    </blockquote></td>

   <td valign="top">

    <blockquote>

     <pre>% <b>more <a href="http://nifty.stanford.edu/2014/wayne-purple-america/data/NJ.txt">NJ.txt</a>                      </b> -75.560143   38.928589 -73.894402   41.35733021AtlanticNJ127 -74.877563   39.608414 -74.736694   39.729721 -74.676102   39.691162  ... -74.857353   39.420528 -74.856087   39.424465 -74.985443   39.514725...WarrenNJ121 -75.120819   40.968208 -75.122986   40.970055 -75.131744   40.969185  ... -75.095901   40.924057 -75.112061   40.948017 -75.118141   40.952927</pre>

    </blockquote></td>

   <td valign="top">

    <blockquote>

     <pre>% <b>more <a href="http://nifty.stanford.edu/2014/wayne-purple-america/data/USA-county.txt">USA-county.txt</a></b>-124.731216   24.544102 -66.980385   49.3843653206AutaugaAL118 -86.916969   32.664028 -86.816589   32.659988 -86.713409   32.661602  ... -86.916809   32.649662 -86.917458   32.653877 -86.921387   32.655415...WestonWY11-105.078743   44.176205-104.375000   44.181641-104.054001   44.180401  ...-105.081238   43.592144-105.078255   43.827049-105.080872   43.826954</pre>

    </blockquote></td>

  </tr>

 </tbody>

</table>

We note that the number of subregions in <a href="http://nifty.stanford.edu/2014/wayne-purple-america/data/USA.txt">USA.txt</a> is not 50 for two reasons: first, we do not include either Alaska or Hawaii; second, we include an entry for each polygonal subregion—some states (such as Michigan, Florida, and California) comprise several polygonal subregions.

<b>Election return data.</b> We supply election return data (sourced from <a href="http://www.uselectionatlas.org/">Dave Leip’s Atlas of U.S. Presidential Elections</a>) that describes the results for each presidential election, by state and county. Each row consists of four fields, separated by commas: the name of a subregion, the number of votes for the Republican candidate, the number of votes for the Democratic candidate, and the number of votes for the Independent (or third party) candidate.

<table border="0" cellspacing="0" cellpadding="0" bgcolor="#FFFFFF">

 <tbody>

  <tr>

   <td valign="top">

    <blockquote>

     <pre>% <b>more <a href="http://nifty.stanford.edu/2014/wayne-purple-america/data/USA2012.txt">USA2012.txt</a>                </b>Alabama,1255925,795696,22717,Alaska,164676,122640,13179,Arizona,1233654,1025232,47673,Arkansas,647744,394409,27315,California,4839958,7854285,360745,...Virginia,1822522,1971820,60147,Washington,1290670,1755396,99892,West Virginia,417655,238269,14743,Wisconsin,1407966,1620985,39483,Wyoming,170962,69286,8813,</pre>

    </blockquote></td>

   <td valign="top">

    <blockquote>

     <pre>% <b>more <a href="http://nifty.stanford.edu/2014/wayne-purple-america/data/NJ2012.txt">NJ2012.txt</a>                  </b>Atlantic,46522,65600,1222,Bergen,169070,212754,4166,Burlington,87401,126377,2561,Camden,69476,153682,2791,Cape May,25781,21657,655,...Salem,14334,14719,570,Somerset,66603,74592,1985,Sussex,40625,26104,1465,Union,68314,139752,2022,Warren,25744,18745,926,</pre>

    </blockquote></td>

  </tr>

 </tbody>

</table>

You can download all of the geometric and election return data files collectively as <a href="http://nifty.stanford.edu/2014/wayne-purple-america/purple-america-data.zip">purple-america-data.zip</a>.

<b>Part 1.</b> Write a program <tt>White.java</tt> that takes the name of a region as the command-line argument and produces an outline map, as in the examples below:

<table border="0" cellspacing="0" cellpadding="0" bgcolor="#FFFFFF">

 <tbody>

  <tr>

   <td valign="top">

    <blockquote>

     <pre>% <b>java White USA</b></pre>

     <img decoding="async" alt="Red-States, Blue-States" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/white-states.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

      <noscript>

       <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/white-states.png?fit=980%2C250" alt="Red-States, Blue-States" height="250" data-recalc-dims="1">

      </noscript>

    </blockquote></td>

   <td valign="top"><pre>% <b>java White NJ          </b></pre><img decoding="async" alt="Red-Counties, Blue-Counties" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/white-nj.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

     <noscript>

      <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/white-nj.png?fit=980%2C250" alt="Red-Counties, Blue-Counties" height="250" data-recalc-dims="1">

     </noscript></td>

   <td></td>

   <td valign="top"><pre>% <b>java White USA-county</b></pre><img decoding="async" alt="Red-Counties, Blue-Counties" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/white-usa.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

     <noscript>

      <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/white-usa.png?fit=980%2C250" alt="Red-Counties, Blue-Counties" height="250" data-recalc-dims="1">

     </noscript></td>

  </tr>

 </tbody>

</table>

For simplicity, draw the point with longitude <em>x</em> and latitude <em>y</em> at location (<em>x</em>, <em>y</em>) in the plane. Use the bounding box of the region to determine the part of the plane to display in the drawing window and rescale the coordinates accordingly.

<b>Part 2.</b> Write a program <tt>RedBlue.java</tt> that takes two command-line arguments (the name of the region and the year of the election) and produces a red-state blue-state map, as in the examples below:

<table border="0" cellspacing="0" cellpadding="0" bgcolor="#FFFFFF">

 <tbody>

  <tr>

   <td valign="top">

    <blockquote>

     <pre>% <b>java RedBlue USA 2012</b></pre>

     <img decoding="async" alt="Red-States, Blue-States" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/redblue-states.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

      <noscript>

       <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/redblue-states.png?fit=980%2C250" alt="Red-States, Blue-States" height="250" data-recalc-dims="1">

      </noscript>

    </blockquote></td>

   <td valign="top"><pre>% <b>java RedBlue NJ 2012   </b></pre><img decoding="async" alt="Red-Counties, Blue-Counties" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/redblue-nj.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

     <noscript>

      <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/redblue-nj.png?fit=980%2C250" alt="Red-Counties, Blue-Counties" height="250" data-recalc-dims="1">

     </noscript></td>

   <td valign="top"><pre>% <b>java RedBlue USA-county 2012</b></pre><img decoding="async" alt="Red-States, Blue-States" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/redblue-usa.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

     <noscript>

      <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/redblue-usa.png?fit=980%2C250" alt="Red-States, Blue-States" height="250" data-recalc-dims="1">

     </noscript></td>

  </tr>

 </tbody>

</table>

<b>Part 3.</b> A more refined visualization reveals that the United States is not as polarized by geography as suggested in the above visualizations. In 2000, Bob Vanderbei created a <a href="https://en.wikipedia.org/wiki/Purple_America">Purple America</a> map, in which each region is colored in a shade of red, green, and blue, according to the proportion of votes received by each candidate. Specifically, if the Republican, Independent, and Democratic candidates receive <em>a</em><sub>1</sub>, <em>a</em><sub>2</sub>, and <em>a</em><sub>3</sub> votes, respectively, then we draw the subregion using the following formula:



<center>

 <img decoding="async" alt="Shade of red, green, and blue" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple.png?w=980" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple.png?w=980" alt="Shade of red, green, and blue" data-recalc-dims="1">

 </noscript>

</center>Write a program <tt>Purple.java</tt> that takes two command-line arguments (the name of the map and the year of the election) and produces a Purple-America map, as in the examples below:



<table border="0" cellspacing="0" cellpadding="0" bgcolor="#FFFFFF">

 <tbody>

  <tr>

   <td valign="top">

    <blockquote>

     <pre>% <b>java Purple USA</b></pre>

     <img decoding="async" alt="Purple States" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple-states.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

      <noscript>

       <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple-states.png?fit=980%2C250" alt="Purple States" height="250" data-recalc-dims="1">

      </noscript>

    </blockquote></td>

   <td valign="top"><pre>% <b>java Purple NJ         </b></pre><img decoding="async" alt="Purple Counties" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple-nj.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

     <noscript>

      <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple-nj.png?fit=980%2C250" alt="Purple Counties" height="250" data-recalc-dims="1">

     </noscript></td>

   <td></td>

   <td valign="top"><pre>% <b>java Purple USA-county</b></pre><img decoding="async" alt="Purple America" height="250" data-recalc-dims="1" data-src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple-usa.png?fit=980%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

     <noscript>

      <img decoding="async" src="https://i0.wp.com/nifty.stanford.edu/2014/wayne-purple-america/purple-usa.png?fit=980%2C250" alt="Purple America" height="250" data-recalc-dims="1">

     </noscript></td>

  </tr>

 </tbody>

</table>

<b>Extra credit.</b> There are limitless opportunities for creativity, enrichment, and inspiration.

<ul>

 <li>Write a program to screen scrape the election return data from <a href="http://www.uselectionatlas.org/">Dave Leip’s Atlas of U.S. Presidential Elections</a>. Pay careful attention to name clashes between Dave Leip’s site and the U.S. Census (e.g., LaSalle vs. La Salle, Kings County vs. Brooklyn).</li>

 <li>Modify your program to include Hawaii and Alaska.</li>

 <li>Use a <a href="https://en.wikipedia.org/wiki/Map_projection">map projection</a> (such as Mercator, azimuthal, Albers, or Gall-Peters) to transform longitude and latitude coordinates into points in the plane.</li>

 <li>Explore a different color palette (with 5-7 color categories) for coloring the subregions. Here is one <a href="http://cdn.filmschoolrejects.com/images/What-America-Looks-Like-2012-Election-Map-640x454.jpg">example</a>.</li>

 <li>Write the state name in the appropriate place. For large states, draw it in the <em>centroid</em> of the polygon describing the state.</li>

 <li>Create an interactive GUI which displays the election returns for a county as the user hovers over it. You will probably need to add a method to your polygon data type to determine whether a point is inside the polygon.</li>

 <li>Visualize the <em>gradient</em> or change in votes from one election to the next.</li>

 <li>Visualize a different data set by county, e.g., poverty rate, access to Internet, and average price of health care. Or collect data for elections in another country.</li>

</ul>

<hr>

<small><i>This assignment was created by Kevin Wayne, with inspiration from Bob Vanderbei.</i></small>

<address><small>Copyright © 2007–2014.</small></address>