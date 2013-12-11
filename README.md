1	+== Welcome to Rails
2	+
3	+Rails is a web-application framework that includes everything needed to create
4	+database-backed web applications according to the Model-View-Control pattern.
5	+
6	+This pattern splits the view (also called the presentation) into "dumb"
7	+templates that are primarily responsible for inserting pre-built data in between
8	+HTML tags. The model contains the "smart" domain objects (such as Account,
9	+Product, Person, Post) that holds all the business logic and knows how to
10	+persist themselves to a database. The controller handles the incoming requests
11	+(such as Save New Account, Update Product, Show Post) by manipulating the model
12	+and directing data to the view.
13	+
14	+In Rails, the model is handled by what's called an object-relational mapping
15	+layer entitled Active Record. This layer allows you to present the data from
16	+database rows as objects and embellish these data objects with business logic
17	+methods. You can read more about Active Record in
18	+link:files/vendor/rails/activerecord/README.html.
19	+
20	+The controller and view are handled by the Action Pack, which handles both
21	+layers by its two parts: Action View and Action Controller. These two layers
22	+are bundled in a single package due to their heavy interdependence. This is
23	+unlike the relationship between the Active Record and Action Pack that is much
24	+more separate. Each of these packages can be used independently outside of
25	+Rails. You can read more about Action Pack in
26	+link:files/vendor/rails/actionpack/README.html.
27	+
28	+
29	+== Getting Started
30	+
31	+1. At the command prompt, create a new Rails application:
32	+       <tt>rails new myapp</tt> (where <tt>myapp</tt> is the application name)
33	+
34	+2. Change directory to <tt>myapp</tt> and start the web server:
35	+       <tt>cd myapp; rails server</tt> (run with --help for options)
36	+
37	+3. Go to http://localhost:3000/ and you'll see:
38	+       "Welcome aboard: You're riding Ruby on Rails!"
39	+
40	+4. Follow the guidelines to start developing your application. You can find
41	+the following resources handy:
42	+
43	+* The Getting Started Guide: http://guides.rubyonrails.org/getting_started.html
44	+* Ruby on Rails Tutorial Book: http://www.railstutorial.org/
45	+
46	+
47	+== Debugging Rails
48	+
49	+Sometimes your application goes wrong. Fortunately there are a lot of tools that
50	+will help you debug it and get it back on the rails.
51	+
52	+First area to check is the application log files. Have "tail -f" commands
53	+running on the server.log and development.log. Rails will automatically display
54	+debugging and runtime information to these files. Debugging info will also be
55	+shown in the browser on requests from 127.0.0.1.
56	+
57	+You can also log your own messages directly into the log file from your code
58	+using the Ruby logger class from inside your controllers. Example:
59	+
60	+  class WeblogController < ActionController::Base
61	+    def destroy
62	+      @weblog = Weblog.find(params[:id])
63	+      @weblog.destroy
64	+      logger.info("#{Time.now} Destroyed Weblog ID ##{@weblog.id}!")
65	+    end
66	+  end
67	+
68	+The result will be a message in your log file along the lines of:
69	+
70	+  Mon Oct 08 14:22:29 +1000 2007 Destroyed Weblog ID #1!
71	+
72	+More information on how to use the logger is at http://www.ruby-doc.org/core/
73	+
74	+Also, Ruby documentation can be found at http://www.ruby-lang.org/. There are
75	+several books available online as well:
76	+
77	+* Programming Ruby: http://www.ruby-doc.org/docs/ProgrammingRuby/ (Pickaxe)
78	+* Learn to Program: http://pine.fm/LearnToProgram/ (a beginners guide)
79	+
80	+These two books will bring you up to speed on the Ruby language and also on
81	+programming in general.
82	+
83	+
84	+== Debugger
85	+
86	+Debugger support is available through the debugger command when you start your
87	+Mongrel or WEBrick server with --debugger. This means that you can break out of
88	+execution at any point in the code, investigate and change the model, and then,
89	+resume execution! You need to install ruby-debug to run the server in debugging
90	+mode. With gems, use <tt>sudo gem install ruby-debug</tt>. Example:
91	+
92	+  class WeblogController < ActionController::Base
93	+    def index
94	+      @posts = Post.all
95	+      debugger
96	+    end
97	+  end
98	+
99	+So the controller will accept the action, run the first line, then present you
100	+with a IRB prompt in the server window. Here you can do things like:
101	+
102	+  >> @posts.inspect
103	+  => "[#<Post:0x14a6be8
104	+          @attributes={"title"=>nil, "body"=>nil, "id"=>"1"}>,
105	+       #<Post:0x14a6620
106	+          @attributes={"title"=>"Rails", "body"=>"Only ten..", "id"=>"2"}>]"
107	+  >> @posts.first.title = "hello from a debugger"
108	+  => "hello from a debugger"
109	+
110	+...and even better, you can examine how your runtime objects actually work:
111	+
112	+  >> f = @posts.first
113	+  => #<Post:0x13630c4 @attributes={"title"=>nil, "body"=>nil, "id"=>"1"}>
114	+  >> f.
115	+  Display all 152 possibilities? (y or n)
116	+
117	+Finally, when you're ready to resume execution, you can enter "cont".
118	+
119	+
120	+== Console
121	+
122	+The console is a Ruby shell, which allows you to interact with your
123	+application's domain model. Here you'll have all parts of the application
124	+configured, just like it is when the application is running. You can inspect
125	+domain models, change values, and save to the database. Starting the script
126	+without arguments will launch it in the development environment.
127	+
128	+To start the console, run <tt>rails console</tt> from the application
129	+directory.
130	+
131	+Options:
132	+
133	+* Passing the <tt>-s, --sandbox</tt> argument will rollback any modifications
134	+  made to the database.
135	+* Passing an environment name as an argument will load the corresponding
136	+  environment. Example: <tt>rails console production</tt>.
137	+
138	+To reload your controllers and models after launching the console run
139	+<tt>reload!</tt>
140	+
141	+More information about irb can be found at:
142	+link:http://www.rubycentral.org/pickaxe/irb.html
143	+
144	+
145	+== dbconsole
146	+
147	+You can go to the command line of your database directly through <tt>rails
148	+dbconsole</tt>. You would be connected to the database with the credentials
149	+defined in database.yml. Starting the script without arguments will connect you
150	+to the development database. Passing an argument will connect you to a different
151	+database, like <tt>rails dbconsole production</tt>. Currently works for MySQL,
152	+PostgreSQL and SQLite 3.
153	+
154	+== Description of Contents
155	+
156	+The default directory structure of a generated Ruby on Rails application:
157	+
158	+  |-- app
159	+  |   |-- assets
160	+  |   |   |-- images
161	+  |   |   |-- javascripts
162	+  |   |   `-- stylesheets
163	+  |   |-- controllers
164	+  |   |-- helpers
165	+  |   |-- mailers
166	+  |   |-- models
167	+  |   `-- views
168	+  |       `-- layouts
169	+  |-- config
170	+  |   |-- environments
171	+  |   |-- initializers
172	+  |   `-- locales
173	+  |-- db
174	+  |-- doc
175	+  |-- lib
176	+  |   |-- assets
177	+  |   `-- tasks
178	+  |-- log
179	+  |-- public
180	+  |-- script
181	+  |-- test
182	+  |   |-- fixtures
183	+  |   |-- functional
184	+  |   |-- integration
185	+  |   |-- performance
186	+  |   `-- unit
187	+  |-- tmp
188	+  |   `-- cache
189	+  |       `-- assets
190	+  `-- vendor
191	+      |-- assets
192	+      |   |-- javascripts
193	+      |   `-- stylesheets
194	+      `-- plugins
195	+
196	+app
197	+  Holds all the code that's specific to this particular application.
198	+
199	+app/assets
200	+  Contains subdirectories for images, stylesheets, and JavaScript files.
201	+
202	+app/controllers
203	+  Holds controllers that should be named like weblogs_controller.rb for
204	+  automated URL mapping. All controllers should descend from
205	+  ApplicationController which itself descends from ActionController::Base.
206	+
207	+app/models
208	+  Holds models that should be named like post.rb. Models descend from
209	+  ActiveRecord::Base by default.
210	+
211	+app/views
212	+  Holds the template files for the view that should be named like
213	+  weblogs/index.html.erb for the WeblogsController#index action. All views use
214	+  eRuby syntax by default.
215	+
216	+app/views/layouts
217	+  Holds the template files for layouts to be used with views. This models the
218	+  common header/footer method of wrapping views. In your views, define a layout
219	+  using the <tt>layout :default</tt> and create a file named default.html.erb.
220	+  Inside default.html.erb, call <% yield %> to render the view using this
221	+  layout.
222	+
223	+app/helpers
224	+  Holds view helpers that should be named like weblogs_helper.rb. These are
225	+  generated for you automatically when using generators for controllers.
226	+  Helpers can be used to wrap functionality for your views into methods.
227	+
228	+config
229	+  Configuration files for the Rails environment, the routing map, the database,
230	+  and other dependencies.
231	+
232	+db
233	+  Contains the database schema in schema.rb. db/migrate contains all the
234	+  sequence of Migrations for your schema.
235	+
236	+doc
237	+  This directory is where your application documentation will be stored when
238	+  generated using <tt>rake doc:app</tt>
239	+
240	+lib
241	+  Application specific libraries. Basically, any kind of custom code that
242	+  doesn't belong under controllers, models, or helpers. This directory is in
243	+  the load path.
244	+
245	+public
246	+  The directory available for the web server. Also contains the dispatchers and the
247	+  default HTML files. This should be set as the DOCUMENT_ROOT of your web
248	+  server.
249	+
250	+script
251	+  Helper scripts for automation and generation.
252	+
253	+test
254	+  Unit and functional tests along with fixtures. When using the rails generate
255	+  command, template test files will be generated for you and placed in this
256	+  directory.
257	+
258	+vendor
259	+  External libraries that the application depends on. Also includes the plugins
260	+  subdirectory. If the app has frozen rails, those gems also go here, under
261	+  vendor/rails/. This directory is in the load path.
