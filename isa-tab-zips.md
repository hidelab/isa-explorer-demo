# Notes on demo-isa-tab

To prepare ISA Tab files for `demo-isatab-explorer.hidelab.org`

These notes assume that this repo is cloned onto a Unix machine
(Linux, probably).

Put ISA-Tab Zip archives in `zips` directory.

run

    sh bin/prepare-tab zips/_yourziphere_

results appear in `unzip` directory.

## if hosting on demo-isatab-explorer.hidelab.org

Copy files to the `demo-isatab-explorer.hidelab.org` instance.

Since the instance is fronted by an AWS Elastic Load Balancer,
you cannot use the DNS name `demo-isatab-explorer.hidelab.org`
to SSH;
You can find the EC2 instance's
Public DNS and IPv4 address listed on the AWS console EC2 Dashboard.

The unzipped ISA-Tab files should be copied from your local
`unzip` directory to the remote directory `~/isa-explorer/data`.

Once files are copied into `data` the website needs rebuilding:

```
python scripts/build_index.py data      # makes isatab-index.json
npm run build:local
```

Currently the web server is simply running as a `nohup` command.
Use `ps waxwux | grep node` to identify the process id of the
server;
kill it;
and execute the following command from the `isa-explorer`
directory to start a fresh server:

```
nohup node server.js                    # Development server
```

The server does not automatically start if the EC2 instance
restarts,
so if the EC2 instance reboots, or the server crashes
(hasn't happened yet), you will need to run the above command
to start a fresh server.

## How was the demo-isatab-explorer instance configured?

The software is ISA Explorer from the ISA tools team,
cloned from the following git repository:
https://github.com/ISA-tools/isa-explorer

Some small modifications have been made to "white-label" the
website. These changes have been made on the EC2 instance itself
and are not change controlled.

The instance has been configured exactly once, by hand,
resulting in these notes (but see also the notes in the
`isa-explorer` repository):

Better to install `node` and `npm` via `nvm`.

Install `nvm`

```
nvm install 6           # Required for isa-explorer
```

## Per website

```
git clone https://github.com/ISA-tools/isa-explorer.git
cd isa-explorer         # you cloned this, right?
virtualenv venv         # creates a subdir called venv
. venv/bin/activate     # runs script created by virtualenv, above

pip install -r requirements.txt         # Only required once
npm install
```

## For the demo-isatab-explorer.hidelab.org site

Add webpack config for the final URL,
`webpack.config.hidelab.js`.
Add a `npm-script` to build using this config. `build:hidelab`

Removed Branding from the isaexplorer logo,
`assets/img/logo.svg`.

Removed top-banner by editing
`app/js/components/views/error.jsx`,
`app/js/components/views/studies.jsx`.

To run the server:

    NODE_ENV=production node server.js


## Things I have done to the data files:

- put in directories beginning with `sdata`
  (seems not to be necessary, perhaps some Scientific Data convention);
- ¡ Cleaned non-utf8 characters in ISA files;
- ¡ renamed investigation files to `i_Investigation.txt`
- Fixed « α » in Investigation file for Lawrie.
- In Lawrie's investigation file,
  filled in Study Title using Publication title.
- removed all morally empty rows from s_*.txt files
  (doesn't seem to matter)
- ¡ ¡ removed all the ASCII CRs. *rage*
- added a bunch of Comment fields.

Turns out isa-explorer requires

Comment[Data Repository]        ""
Comment[Data Record Accession]  ""
Comment[Data Record URI]        ""

I added a bunch (all the ones from 3t3). That makes the Python
changes redundant.

