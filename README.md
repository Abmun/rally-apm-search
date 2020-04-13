<!-- wp:paragraph -->
<p>For performance benchmarking on the cluster we need to execute search queries on the elasticsearch nodes to measure the latency, response time metrics etc.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I have come up with a custom track to execute search queries specific to APM data covering two use cases-</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>1) Execute search queries on live apm data </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>2) Execute search queries on sample data ingested in the previous section</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The custom track has two challenges specific to these use cases but the search queries can be modified as per requirement in the operations/querying json files.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Create a file params-file.json to provide the runtime of the test in seconds-</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Ex below with runtime of 30 mins.</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>{</code>
<code>"query_time_period": 1800</code>
<code>}</code></pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Command to run test on live data-</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>esrally --track-path=/root/.rally/benchmarks/tracks/rally-apm-search/eventdata --target-hosts=&lt;ES Node IP>:9200,&lt;ES Node IP>:9200,&lt;ES Node IP>:9200 --pipeline=benchmark-only --client-options="use_ssl:true,verify_certs:false,basic_auth_user:'&lt;username>',timeout:120,basic_auth_password:'&lt;password>'" --challenge=apm-search-queries-livedata --track-params=./params-file.json --user-tag="name-env:&lt;Name>-&lt;Env>"</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>Command to run test on sample data-</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>esrally --track-path=/root/.rally/benchmarks/tracks/rally-apm-search/eventdata --target-hosts=&lt;ES Node IP>:9200,&lt;ES Node IP>:9200,&lt;ES Node IP>:9200 --pipeline=benchmark-only --client-options="use_ssl:true,verify_certs:false,basic_auth_user:'&lt;username>',timeout:120,basic_auth_password:'&lt;password>'" --challenge=apm-search-queries-sampledata --track-params=./params-file.json --user-tag="dc-env:&lt;Name>-&lt;Env>"</code></pre>
<!-- /wp:code -->
