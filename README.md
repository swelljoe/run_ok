# run_ok
Run, OK? is a shell function to run a function with pretty output. It produces a Unicode checkmark or X if the shell supports it (we don't check the terminal, but terminals seem to be more likely to support it than shells), and an "OK!" or "ERROR" otherwise. They will be green, and red, respectively, assuming the terminal supports color and the palette being used has reasonable greenish and reddish colors in the right places.

It is expected to work in reasonably modern bash and dash. I will try to test occasionally on FreeBSD Bourne sh, but right now, I can't make FreeBSD run in Vagrant for more than a few seconds.

# What's it look like?

![run_ok demo](http://i.imgur.com/7gcOilK.gif)

# Usage

Source it, and call your long-running processes, using the run_ok function:

```bash
    . ./run_ok.sh
    
    # Where to log results
    log=/path/to/run.log
    
    run_ok "do --something --slow" "Doing something slow"
```

Currently there's only one obvious knob to twiddle in run_ok, which is the log file. It requires [spinner](http://github.com/swelljoe/spinner) to be installed in the parent directory (you can adjust that in the run_ok.sh source).

But, you can also override spinner option variables. See the spinner docs for what those are. The "WIDE" spinners are designed to work nicely with run_ok.

# Compatibility

This one is really tricky, on a lot of fronts. Unicode, argument passing, fractional second sleep, etc. are all of questionable cross-platform availability. But, it works in my tests on the platforms and versions I need to support.

I am confident it works on reasonably modern bash and dash (where I test with every change). I am less confident of Bourne sh on FreeBSD.

# Contributing

I welcome patches, as long as they don't break compatibility with bash and dash. I especially welcome patches that improve compatibiltiy across other shells, or make run_ok more resilient to odd input. (In particular, I don't know how to pass in a multi-expression command, e.g. with ; to separate commands, and would like to support that use case, though error capture would be particularly tricky).
