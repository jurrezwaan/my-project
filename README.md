[![Run tests](https://github.com/jurrezwaan/my-project/actions/workflows/run_test.yml/badge.svg)](https://github.com/jurrezwaan/my-project/actions/workflows/run_test.yml)

<center><div class="readability"><h1 id="github-actions">GitHub Actions</h1>
<p>GitHub has a feature called Actions, which is a way of automating tasks that come up as a result of writing code. The wording here is deliberately open-ended; you can do almost
anything that you can do on your own computer in GitHub Actions, but in an automated way. Some examples of things that you may want to automate are:</p>
<ul>
<li>Running tests on the code every time a new commit is pushed to GitHub to make sure everything is working;</li>
<li>Checking if there have been reports of new security problems with libraries you use every morning;</li>
<li>Indexing how much of the code in your repository is covered by tests you wrote, and display a badge showing the percentage in the <code>README</code>;</li>
<li>Automatically update code running on servers whenever you pushed a commit to a certain branch;</li>
<li>Running your code after every push and upload the result to a web server.</li>
</ul>
<p>A workflow is defined in a <code class="interpreted-text" role="term">YAML</code> file, a common configuration file format that you can think of as a structured list. It looks
like this:</p>
<div class="sourceCode" id="cb1">
<pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="fu">name</span><span class="kw">:</span><span class="at"> Bob Bobbiton</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="co"># A comment. We can write something here to clarify what we wrote below.</span></span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a><span class="fu">birth-date</span><span class="kw">:</span><span class="at"> 1970-12-31</span></span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a><span class="fu">friends</span><span class="kw">:</span></span>
<span id="cb1-7"><a href="#cb1-7" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">alice</span><span class="kw">:</span></span>
<span id="cb1-8"><a href="#cb1-8" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">name</span><span class="kw">:</span><span class="at"> Alice Aliceton</span></span>
<span id="cb1-9"><a href="#cb1-9" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">location</span><span class="kw">:</span><span class="at"> London</span></span>
<span id="cb1-10"><a href="#cb1-10" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">steve</span><span class="kw">:</span></span>
<span id="cb1-11"><a href="#cb1-11" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">name</span><span class="kw">:</span><span class="at"> Steve Steveton</span></span>
<span id="cb1-12"><a href="#cb1-12" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">location</span><span class="kw">:</span><span class="at"> Glasgow</span></span></code></pre></div>
<p>GitHub Actions needs to know two things from the YAML file in order to run the workflow:</p>
<ul>
<li><strong>Triggers</strong>: when should it run? Trigger events fall roughly into three categories:
<ul>
<li><em>Scheduled</em>: every Tuesday at 10:15.</li>
<li><em>Manual</em>: use a button in the web interface to trigger a workflow.</li>
<li><em>Incidental events</em>: it will run whenever some specific event happens, like a new push or pull request, or when the repository is forked.</li>
</ul>
</li>
<li><strong>Jobs</strong>: what should it do? This consists of a number of steps that are executed in order.</li>
</ul>
<h2 id="your-first-github-action">Your First GitHub Action</h2>
<p>Here's what a workflow looks like that is <strong>manually triggered</strong> and runs one <strong>job</strong>: a simple print statement.</p>
<div class="sourceCode" id="cb2">
<pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb2-1"><a href="#cb2-1" aria-hidden="true" tabindex="-1"></a><span class="fu">name</span><span class="kw">:</span><span class="at"> Print Hello</span></span>
<span id="cb2-2"><a href="#cb2-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-3"><a href="#cb2-3" aria-hidden="true" tabindex="-1"></a><span class="fu">on</span><span class="kw">:</span><span class="at"> workflow_dispatch</span></span>
<span id="cb2-4"><a href="#cb2-4" aria-hidden="true" tabindex="-1"></a><span class="fu">jobs</span><span class="kw">:</span></span>
<span id="cb2-5"><a href="#cb2-5" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">print-hello</span><span class="kw">:</span></span>
<span id="cb2-6"><a href="#cb2-6" aria-hidden="true" tabindex="-1"></a><span class="co">    # Specify on which operating system we want this workflow to run</span></span>
<span id="cb2-7"><a href="#cb2-7" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">runs-on</span><span class="kw">:</span><span class="at"> ubuntu-20.04</span></span>
<span id="cb2-8"><a href="#cb2-8" aria-hidden="true" tabindex="-1"></a><span class="co">    # The steps that will be excuted</span></span>
<span id="cb2-9"><a href="#cb2-9" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">steps</span><span class="kw">:</span></span>
<span id="cb2-10"><a href="#cb2-10" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="kw">-</span><span class="at"> </span><span class="fu">name</span><span class="kw">:</span><span class="at"> Print</span></span>
<span id="cb2-11"><a href="#cb2-11" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="fu">run</span><span class="kw">:</span><span class="at"> echo "Hello, world!"</span></span></code></pre></div>
<p>Workflows go into the <code class="interpreted-text" role="file">.github/workflows/</code> folder relative to the root of your repository. To run this workflow, follow these
steps:</p>
<ol type="1">
<li>Create a new directory <code class="interpreted-text" role="file">my-project</code>.</li>
<li>Within it, paste the above YAML text into <code class="interpreted-text" role="file">.github/workflows/hello.yml</code>. You should have this file structure:</li>
</ol>
<pre class=""><code>.
└── .github
    └── workflows
        └── hello.yml</code></pre>
<ol type="1" start="3">
<li>Add and commit your changes and push them to an empty repository on GitHub.</li>
<li>Go to the repository's page on GitHub in your browser.</li>
<li>Go to the repository's <em>Actions</em> tab.</li>
<li>Under <em>All Workflows</em>, you should see <em>Print Hello</em>. Click it.</li>
<li>Run the workflow using the <em>Run workflow</em> button on the right.</li>
<li>Refresh the page. You should see that the workflow run has been requested. Click that new line.</li>
<li>Click the name of the job on the left side (<code>print-hello</code>) to see how running it went.</li>
</ol>
<p>Here you should see a dark screen with three components:</p>
<ul>
<li>Set up job</li>
<li>Print</li>
<li>Complete job</li>
</ul>
<p>These are the steps that the workflow went through during execution. All workflows go through at least the <em>Set up</em> and <em>Complete</em> steps. The rest of the steps
are defined by you, the user. You can click into each step to see exactly which commands were run and what their output was. Notice the print statement on line <code>1</code>
within the <em>Print</em> step and its output on line <code>4</code>!</p>
<h2 id="doing-more-with-actions">Doing More With Actions</h2>
<p>Alright, we now know about the bare bones of workflows on GitHub Actions. Let's do something a little more useful than printing a line.</p>
<p>For most workflows it makes sense to want access to your repository. It's entirely possible to write a script to clone your repository and run it in the same way that we just
printed <code>Hello, world!</code>. But in Actions, there is a better way: use an Action!</p>
<p>GitHub Actions gets its name from the idea of sharing different Actions across all users of the service. An 'Action' lives in a repository by itself. While you can build your
own, there are already <em>many</em> actions out there you can use. Let's use an Action supplied by GitHub itself to bring the repository we are working with into the workflow
environment.</p>
<div class="sourceCode" id="cb4">
<pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb4-1"><a href="#cb4-1" aria-hidden="true" tabindex="-1"></a><span class="fu">name</span><span class="kw">:</span><span class="at"> Checkout Example</span></span>
<span id="cb4-2"><a href="#cb4-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb4-3"><a href="#cb4-3" aria-hidden="true" tabindex="-1"></a><span class="fu">on</span><span class="kw">:</span><span class="at"> workflow_dispatch</span></span>
<span id="cb4-4"><a href="#cb4-4" aria-hidden="true" tabindex="-1"></a><span class="fu">jobs</span><span class="kw">:</span></span>
<span id="cb4-5"><a href="#cb4-5" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">checkout-repository</span><span class="kw">:</span></span>
<span id="cb4-6"><a href="#cb4-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">runs-on</span><span class="kw">:</span><span class="at"> ubuntu-20.04</span></span>
<span id="cb4-7"><a href="#cb4-7" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">steps</span><span class="kw">:</span></span>
<span id="cb4-8"><a href="#cb4-8" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="kw">-</span><span class="at"> </span><span class="fu">name</span><span class="kw">:</span><span class="at"> Checkout repository</span></span>
<span id="cb4-9"><a href="#cb4-9" aria-hidden="true" tabindex="-1"></a><span class="at">        </span><span class="fu">uses</span><span class="kw">:</span><span class="at"> actions/checkout@v2</span></span></code></pre></div>
<p>That's it! After the <code>Checkout repository</code> step the repository can be found in <code>$GITHUB_WORKSPACE</code>.</p>
<div class="note">
<div class="title">
<p>Note</p>
</div>
<p>Here <code>GITHUB_WORKSPACE</code> is a shell environment variable. When we write <code>$GITHUB_WORKSPACE</code> we mean 'the value of environment variable
<code>GITHUB_WORKSPACE</code>'. This way you never really need to know where the repository is located in absolute terms. Whenever you want to specify the repo's location, just
write <code>$GITHUB_WORKSPACE</code> instead. For example: <code>cd $GITHUB_WORKSPACE</code>.</p>
</div>
<h2 id="horizon">Horizon</h2>
<p>There is almost no limit to what you can do with GitHub Actions. Explore the <a href="https://github.com/marketplace?type=actions">GitHub Actions Marketplace</a> and <a href="https://docs.github.com/en/free-pro-team@latest/actions">the documentation</a> to learn about Actions different trigger events, inputs and outputs, artifacts and more.</p></div></center>
