CHANGELOG
=========

2.0.0 (2019-05-22)
------------------

### Backend
- Some AJAX requests are marked as to-be-cached for a little amount of time so that server load decreases when you need many tabs open.

### Pages

#### Configuration
- "Save Configuration" button reloads the bots whose destination queues changed (#175).
- Allow standard vis.js arrow and +/- navigation when network chart is focused (#176).
- Underscored letters denote shortcuts - you can now edit the network without wandering the mouse all around the screen (#176).
- Correctly load JSON parameters when editing a bot: content instead of '[object Object]' string.
- Handle not explicitly given internal queues.
- Physics / Live button are now rememberable in the positions.conf file on the server.
- When changing state or being disabled or erroneous, bot receives dashed border.
- You are allowed to create multiple edges between the same nodes - correctly displayed. If the edges should have the same paths, rename dialog appears.

#### Management
- Auto-reloading
- Clicking an action on a bot will make group panel correspond immediately
- Clicking an action on a panel will make group in the table correspond immediately

#### Monitor
- Correctly display JSON parameters: content instead of '[object Object]' string.
- Reloading logs fixed
- Reloading logs every 3 sec instead of 300 sec
- Auto-reloading logs after bot started/stopped

### Documentation
- Add SECURITY.md file.

### Known issues
* Missing CSRF protection (#111).
* Graph jumps around on "Add edge" bug component (#148).
* wrong error message for new bots with existing ID (#152).


1.1.0 (2018-11-12)
------------------
- Add generic MIT license text to make `reuse` license checker happy (#140).

### Backend
* Using LESS for writing CSS (so CSS is now readonly)
* Fix on several places: intervals won't flood server if there is a lag, they'll wait till previous request has finished. Auto-delay/boost depending on server lag.

### Frontend
* Error reporting in a less-disturbing text box rather than an tab-wide javascript alert. Click to enlarge, double click to hide.
* Much more detailed Error reporting. What was earlier just mere 'SyntaxError: JSON.parse ...' has now included 'Failed to execute intelmqctl:~/.local/bin/intelmqctl --type json list queues' - see? That's a full command that'll help the developer so much in debugging. (Long error reports got automatically truncated to 200 characters.)
* If an error appears again and again (redis down?) it blinks instead of spamming you, updates its time and show number of times it has been thrown.
* Current tab marked in menu

### Pages

#### Configuration
* New menu item linking selected bot with the monitor (just an icon to preserve space on precious menu bar). Supports ctrl+click to new tab on the whole button area.
* New menu item to duplicate current bot, its queues included (and focus the new one); the new bot is selected and focused so that the user finds it on a big plan. It is inserted instead of the add button when a bot is selected.
* You may now see live data, each bot has its queue length in the label
* Button labels (Add bot, Add queue instead of Add node, Add edge) now makes more sense and won't shock a newcomer
* Clearly visible bot statuses; if bot is not running, its colour is dimmed.
- Manager now supports named queue paths. They are displayed along the edges and editable.
- Double click edits the bot or the queue
- Code cleanup: New modal window for performing multiple dialog actions. Intercepting visjs internals without using external Hammer library.
- Enter key submits the edit bot dialog.
- Clicking on the side-menu bot name cycles amongst bot instances in the canvas.
- Got rid of the dumb "#load" and "#new" parameter → "#new" converted into a standard URL parameter "configuration=new".
- Button to turn on/off physics
- Detection for bots not configured in runtime but in pipeline configuration (#166).
- Runtime parameters with the names 'group', 'name' or 'module' were not editable (they are read-only for the 'generic' section) (#172).
- Message counter for removed queues is correctly reset (#158).

#### Management
* Control buttons (start/stop...) now are not only part of the management tab but are common even for configuration tab and inspection panel in monitor tab. They need less configuration (thanks to $(document).on global configuration feature) and works better with less code used (single method instead of four of them). There is also a new red state 'error' for non-standard problems or invalid output from intelmqctl.
* Clicking bot name support ctrl+click to new tab
* Table doesn't redraw all the time (so that a highlighting of a browser search is preserved while clicking on a button)
* It is now possible to start/stop a group of bots easily. Additional panels are linked, so that if you eg. start all the experts, but let other bots stopped, Experts panel shows that all bots are running and Botnet panel shows that only some bots are running.

#### Monitor
* Fixed bot crawling in Monitor section (F5 will take you on the same page, not on the main monitoring page, permanent links, history browsing)
* Prefer updating the destination queues overview table over redrawing it all the time (so that you can select some text)
* Reloading a page sometimes caused a disturbing 'Error loading' alert in Firefox if an AJAX request had not yet been completed
* Fixed bug: when clicking on bot destination queue in bot detail, we won't end in an undefined bot
* Inspect panel allows you to communicate via debug functions of `intelmqctl` (see and inject messages, process single message and see output). Ctrl+Enter hits the Process button (hint included in textarea placeholder). Checkbox 'Inject message from above' marked on first text ever written to message textarea.
* The new parameters panel that displays the bot's parameters on the bot's monitor page. For parameters which are filenames, the content of these files will be shown as text if they reside in the allowed paths (set in config.php).
* When needed, Path column appears, resizing the Queues panel accordingly.
* Connected with the configuration panel → a link appears next to the bot title that takes you directly to the bot

### Known issues
* Missing CSRF protection (#111).
* Graph jumps around on "Add edge" bug component (#148).
* wrong error message for new bots with existing ID (#152).

1.0.2 (2018-09-24)
------------------

### Backend
- Emit a more specific error message for cases like #160.
- The timeout for calls to `intelmqctl` has been raised to 20s (#164).

### Pages

#### Configuration
- Underscore is now allowed for new parameter names (#153).

#### Monitor
* Fix link to monitor page (#157).

### Documentation
- Add a FAQ and add a section about the docker issue (#160).
- Add instructions for Debian 9, Ubuntu 18.04, and openSUSE Leap 42.3, 15.0 (#168).

### Packaging
- Include a positions file matching the default configuration of intelmq (#171).

### Known issues
* Missing CSRF protection (#111).
* Missing copyright notices (#140).
* Graph jumps around on "Add edge" bug component (#148).
* wrong error message for new bots with existing ID (#152).
* Queue size for deleted queue remains displayed (#158).

1.0.1 (2018-04-23)
------------------
The version is compatible with intelmq >= 1.0.3

### Backend
* Fix version number.

### Known issues
* Missing CSRF protection (#111).
* Missing copyright notices (#140).
* Graph jumps around on "Add edge" bug component (#148).
* new runtime parameters with _ not possible (#153).
* wrong error message for new bots with existing ID (#152).

1.0.0 (2018-04-23)
------------------
The version is compatible with intelmq >= 1.0.3

### Backend
* Set content type correctly for JSON data in configuration loading (#112)

### Pages
* All pages are now deliverd by php, reducing the amount of duplicate code drastically.

#### Landing page
* Added a new block for the new check page, changed the formatting a bit.

#### Configuration
* Fixed handling of special parameter `run_mode` (#150)
* Intelmqctl controller may be set via an env variable `INTELMQ_MANGER_CONTROLER_CMD`

#### Check
* Added, showing the output of `intelmqctl check` (#118).

### Documentation
* Note on header Content-Security-Policy (#113)
* Note on security considerations in Readme to avoid misunderstandings
* Remove compatibility warning from README

### Third-party libraries
* reverted update jQuery to 3.2.1
* reverted update metisMenu to 2.7.0

### Licenses
* Licenses of used and included software is now inventarized and properly declared in LICENSES/ (#134)

### Packaging
* fix packaging of positions.conf file for deb-packages (#133).

### Known issues
* Missing CSRF protection (#111).
* Missing copyright notices (#140).
* Graph jumps around on "Add edge" bug component (#148).
* new runtime parameters with _ not possible (#153).
* wrong error message for new bots with existing ID (#152).

0.3.1 (2017-09-26)
------------------
### Configuration
* Fixed validation on files before saving them, this has rejected valid data

0.3 (2017-09-25)
----------------
* Partly support for CentOS/RHEL 7 (#55, #103)
* Note on security considerations in Readme to avoid misunderstandings
* Show versions of intelmq and intelmq manager on about page
* Update vis.js to current version
* update jQuery to 3.2.1
* update metisMenu to 2.7.0

### Configuration
* interface for defaults.conf (#45)
* drag&drop (#105, #41)
* fix #96
* save buttons starts blinking after changes (#41)
* Allow redrawing of botnet on demand
* Save/load position of bots in/from /opt/intelmq/etc/manager/positions.conf
  File needs to be writeable
* parameters from defaults are shown for new bots (#107)
* parameters are grouped by type: generic, runtime, defaults
* better feedback on errors with backend (#69, #99)
* pressing ESC in forms equals to pressing the cancel button
* Edit node window is now much bigger
* pressing enter in 'add key' window equals to pressing ok button

### Management
* Reload and restart have been added as actions on bots and the whole botnet (#114)
* A click on the bot name opens the monitor page of the bot

### Monitor
* clearing queues is possible in general and specific view for all queues (#54)

### Backend
* Fix regex checks on bot ids and log line number in controller, they have not been effective
* fix overflow in extended message box (#49)

0.2.1 (2017-06-20)
------------------
* Fix syntax error in pipeline.js preventing loading of configuration page

0.2.0 (2017-06-20)
------------------
* first release
