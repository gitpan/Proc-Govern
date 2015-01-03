* TODO [2015-01-03 Sat] procgov: Govern multiple processes instead of just one

  It's only natural that we expand to this, to reduce the number of monitor
  process.
  
  We want to be able to set options for all processes or on a per-process basis.
  For example: when load watching, all processes can be stopped and resumed using
  the same high/load criteria, but some processes might want to have a different
  criteria. The same goes with timeout.
  
  Some options are for a per-process, e.g. capturing stderr.
  
  If we support multiple commands, e.g. C<< commands => ['cmd1', ['cmd2', 'arg']]
  >> then we'll also need to return exit codes for each command, e.g. C<< [0, 124]
  >>.
  
  We should exit only after all child processes terminate. But when a child exits,
  a hook can be defined e.g. C<on_child_exit>.
* TODO [2015-01-03 Sat] procgov: Allow specifying time point (instead of duration) for timeout?

  For example, we might want to say "this command should not run past midnight".
  
  In general, we might also want to allow specifying a coderef for flexible
  timeout criteria?
* TODO [2015-01-03 Sat] procgov: Print messages when stopping/resuming due to load control

  Like B<loadwatch> does:

       Fri Mar 14 16:17:52 2014: load too high, stopping.
       Fri Mar 14 16:18:52 2014: load low, continuing.
* TODO [2015-01-03 Sat] procgov: Option to not use File::Write::Rotate for logging STDOUT/STDERR

  If command is output-heavy, FWR will become a significant overhead. Unless FWR
  has the option of skipping logging (I'm contemplating on this) ...
* IDEA [2014-03-18 Tue] procgov: option to feed stdin to command
* TODO [2014-09-06 Sat] procgov: load control: option utk STOP & START semua children/descendants

  karena mis gw 'govproc --load-low 1 --load-high 2 sync-media-from-seagate2' tapi
  ternyata load terus sampe 4+, proses rsync tetap berjalan walaupun
  sync-media-from-seagate2 dalam keadaan stopped (T).
  - log ::
    + [2014-09-06 Sat] done, option killfam.
* IDEA [2014-09-06 Sat] procgov: option utk time process

  - seperti unix utility 'time', tapi mungkin ada advanced options-nya. time cpu
    sys/usr, beserta anak cucu, time secara berkala utk dapat graph.
