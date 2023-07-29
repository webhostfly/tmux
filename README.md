## What is tmux?

Tmux is a **terminal multiplexer**. It creates a host **server** on your Linode and connects to it with a client window. If the client is disconnected, the server keeps running. When you reconnect to your Linode after rebooting your computer or losing your Internet connection, you can reattach to the tmux session and the files you were working with will still be open, and the processes you had running will still be active.

By attaching multiple sessions, windows, and panes to a tmux server, you can organize your workflow and easily manage multiple tasks and processes.

**Installation**:  
Make sure tmux is installed on your Linux system. If it's not already installed, you can install it using your package manager. For example, on Debian/Ubuntu-based systems, you can use:

### Debian or Ubuntu:

Install tmux on CentOS by using the apt package manager:

```plaintext
sudo apt install tmux
```

### CentOS:

Install tmux on CentOS by using the yum package manager:

```plaintext
yum install tmux
```

### Mac OSX:

Install tmux on Mac OS X by using Homebrew:

```plaintext
brew install tmux
```

**Starting a new session**:  
To start a new tmux session, simply open a terminal and type:

This will create a new session with a single window.

**Basic tmux commands**:

*   To execute a command within tmux, you'll need to use a special key combination. By default, tmux uses `Ctrl + b` as the prefix key. So, to issue a command, you would press `Ctrl + b`, and then the command key.
*   For example, to create a new window, you would press: `Ctrl + b`, and then `c`.
*   To close the current window, press: `Ctrl + b`, and then `&`.
*   To detach from the current session (keeping it running in the background), press: `Ctrl + b`, and then `d`.

**Navigating windows**:

*   To navigate between windows, use `Ctrl + b`, and then one of the arrow keys (`Up`, `Down`, `Left`, or `Right`).
*   To switch to a specific window, use `Ctrl + b`, and then the window number (e.g., `0` for the first window, `1` for the second, and so on).

**Splitting panes**:

*   To split the current pane horizontally, use `Ctrl + b`, and then `%`.
*   To split the current pane vertically, use `Ctrl + b`, and then `"`.
*   To switch between panes, use `Ctrl + b`, and then the arrow keys in the direction you want to move.

**Resizing panes**:

To resize panes, first, press `Ctrl + b`, and then `:` to bring up the command prompt.

Then, use the `resize-pane` command followed by an optional argument to specify the size. For example, to resize a pane 10 lines up, you can use:

Similarly, you can use `-D` for down, `-L` for left, and `-R` for right.

**Closing panes**:

*   To close the current pane, simply type `exit` or use `Ctrl + d`.

**Exiting tmux**:  
To exit tmux entirely (and all its sessions), ensure that all windows and panes are closed, and then simply type `exit` in the last remaining pane.

**Reattaching to a session**:  
To reattach to a detached session, use the following command:

If you had multiple sessions running, you can specify the session's name to reattach to a specific one:

If you want to attach to a session that is already attached elsewhere, you can use:

This will detach the other connection and allow you to attach to the session.

These are some of the basic tmux commands to get you started. Tmux is highly customizable, and you can create complex workflows using its various features. To learn more about tmux and its advanced capabilities, you can refer to the man pages (`man tmux`) or online tutorials and documentation.

```plaintext
tmux attach-session -d
```

```plaintext
tmux attach-session -t session_name
```

```plaintext
tmux attach
```

```plaintext
resize-pane -U 10
```

```plaintext
tmux
```

Detach from the session:

This will return you to the basic terminal.

To attach to the last session you used, run:

The command `tmux a` can be used as well. To attach to a specific session, run `tmux attach -t $name`, replacing _$name_ with the unique name given to the session you wish to use.

Once a session has been started, it will continue to run as long as the Linode is running or until you stop the session.

## tmux Commands

There are three ways to issue commands to tmux:

**shortcuts**: tmux uses what is called a _prefix key_, which is `CTRL+b` by default. tmux will interpret the keystroke following the prefix as a tmux shortcut. For example: to detach from your session using a shortcut: press `CTRL+b`, release both keys and then press `d`.

**command mode**: Enter command mode by pressing the prefix followed by `:`. This will open a command prompt at the bottom of the screen, which will accept tmux commands.

**command line**: Commands can also be entered directly to the command line within a tmux session. Usually these commands are prefaced by `tmux`. The `tmux attach` command used in the previous section was an example of this type of command.

Most tmux tasks can be accomplished using any of these three methods.

{{\< note respectIndent=false >}}  
You can change the prefix key by editing the `~/.tmux.conf` file. For the remainder of this guide, **Prefix** will be used to refer to either the default `CTRL+b` or the combination you have chosen in your configuration file.  
{{\< /note >}}

### Getting Help with tmux by Reviewing Keyboard Shortcuts

At any time, you can display tmux keyboard shortcuts by entering your prefix followed by `?`:

```plaintext
Prefix + ?
```

## Manage tmux Windows

When a tmux session starts, a single window is created by default. It is possible to attach multiple windows to the same session and switch between them as needed. This can be helpful when you want to run multiple jobs in parallel.

| Command | Result |
| --- | --- |
| **Prefix** + **c** | Create a new window |
| **Prefix** + **p** | Switch to the previous window |
| **Prefix** + **n** | Switch to the next window |
| **Prefix** + **0-9** | Switch to a window using it's index number |
| **Prefix** + **w** | Choose a window from an interactive list |
| **exit** | Close a window |
| **Prefix** + **&** | Force kill-all processes in an unresponsive window |
| **Prefix + %** | Split windows horizontally |
| **Prefix + “** | Split windows vertically |
| **Prefix + M-n** | Switch between windows. Switching to a window that has a content alert, an activity or a bell |
| **Prefix + M-p** | Switch back to a previous window that has a content alert, an activity or a bell |

By default, tmux names each window according to the process that spawned it (most commonly bash). To give windows names that are easier to remember and work with, you can rename a window with **Prefix + ,**.

## Manage tmux Panes

Each window can be divided into multiple panes. This is useful when you want outputs from multiple processes visible within a single window.

| Command | Result |
| --- | --- |
| **Prefix** + **"** | Split the active pane horizontally |
| **Prefix** + **%** | Split the active pane vertically |
| **Prefix** + **arrow key** | Switch to another pane |
| **Prefix** + **ALT+arrow** | Resize the active pane |
| **Prefix** + **z** | Zoom in on the active pane. Press the same combination again to exit zoom mode |
| **exit** | Close the active pane |
| **Prefix** + **x** | Force kill an unresponsive process in a pane |
| **Prefix + k** | To move the pane above |
| **Prefix + j** | To move the pane below |
| **Prefix + h** | To move the left panes |
| **Prefix + l** | To move the right pane |
| **Prefix + q** | Display pane numbers |
| **Prefix + o** | Toggle / jump to the other pane |
| **Prefix + }** | swap current pane with the pane from the left |
| **Prefix + {** | swap current pane with the page from the right |
| **Prefix + !** | move the pane out of current window |
| **Prefix + ;** | Go to the last used pane |
| **Prefix + M-1** | Predefined layout to switch to even-horizontal layout |
| **Prefix + M-2** | Predefined layout to switch to even-vertical layout |
| **Prefix + M-3** | Predefined layout to switch to main-horizontal layout |
| **Prefix + M-4** | Predefined layout to switch to main-vertical layout |
| **Prefix + M-5** | Predefined layout to switch to a tiled layout |
| **Prefix + space** | Predefined layout to switch to the next layout |
| **Prefix + C-o** | To move all panes, rotating the window up |
| **Prefix + M-o** | To move all panes, rotating the window down |
| **tmux bind-key k resize-pane -U \[i\]** | To move the divider up i lines (for horizontal divider) |
| **tmux bind-key k resize-pane -D \[i\]** | To move the divider down i lines (for horizontal divider) |
| **tmux bind-key k resize-pane -L \[i\]** | To move the divider left i columns (for vertical divider) |
| **tmux bind-key k resize-pane -R \[i\]** | To move the divider right i columns (for vertical divider) |
| **C-a C-up, C-a C-down, C-a C-left, C-a C-right** | To resize panes by 1 row/column |
| **C-a M-up, C-a M-down, C-a M-left, C-a M-right** | To resize panes by 5 rows/columns |

## Manage tmux Sessions

Sometimes even multiple windows and panes aren't enough and you need to separate the layouts logically by grouping them into separate sessions. Open the command prompt with **Prefix** then **:**, then start a new session:

```plaintext
new-session
```

{{\< note respectIndent=false >}}  
It's also possible to type shorter versions of a command, for example: "new-se". But this will work only if there isn't another command that starts with the same string of characters.  
{{\< /note >}}

| Command | Result |
| --- | --- |
| **Prefix** + **(** | Switch to the previous session |
| **Prefix** + **)** | Switch to the next session |
| **Prefix** + **s** | Display an interactive session list |
| **Prefix + d** | detach from the current session |
| **Prefix + $** | rename a session in tmux |
| **Prefix + L** | Select the most recently used session (or the last session). Use the same combination again to return. |
| `tmux ls` | List all available sessions |
| `tmux kill-server` | Destroy all sessions and kill all processes |

## Create a tmux Configuration File

1.  As you get comfortable with tmux, you may want to change some of the defaults. Using a text editor, create a configuration file in your user's home directory:

Other configuration options are available in the [tmux manual](http://man.openbsd.org/OpenBSD-current/man1/tmux.1).

## Servers in Tmux

Whenever you launch tmux, a server is initiated. You can connect to a tmux server under a specific socket name by using the command `tmux -L <socket name>`. For example, to connect to a server with the socket name “linode\_socket”, run the following command:

```plaintext
tmux -L linode_socket
```

This attaches a new session. If a session already exists and want to attach to it, run the following command instead:

```plaintext
tmux -L linode_socket attach
```

```plaintext
source-file ~/.tmux.conf
```

```plaintext
 tmux attach
```

```plaintext
 tmux detach
```

```plaintext
tmux
```
