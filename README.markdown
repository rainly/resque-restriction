resque-restriction
===============

Resque Restriction is a plugin for the [Resque][0] queueing system (http://github.com/defunkt/resque). It adds two functions:

1. it will limit the execution number of certain jobs in a period time. For example, it can limit a certain job can be executed 1000 times per day, 100 time per hour and 30 times per 300 seconds.

2. it will execute the exceeded jobs at the next period. For example, you restrict the email sending jobs to run 1000 times per day. If your system generates 1010 email sending jobs, only 1000 email sending jobs can be executed today, and the other 10 email sending jobs will be executed tomorrow.

Resque Restriction requires Resque 1.7.0.

To use
------

It is especially useful when a system has an email invitation resque job, because sending emails too frequentyly will be treated as a spam. What you should do for the InvitationJob is to inherit it from Resque::Plugins::RestrictionJob class and add restrict definition. Example:

	class InvitationJob < Resque::Plugins::RestrictionJob
	  restrict :per_day => 1000, :per_hour => 100, :per_300 => 30

	  #rest of your class here
	end

That means the InvitationJob can not be executed more than 1000 times per day, 100 times per hour and 30 times per 300 seconds.

The argument of restrict method is a hash, the key of the hash is a period time, including :per_minute, :per_hour, :per_day, :per_week, :per_month, :per_year, and you can also define any period like :per_300 means per 300 seconds. the value of the hash is the job execution limit number in a period.

Contributing
------------

Once you've made your commits:

1. [Fork][1] Resque Restriction
2. Create a topic branch - `git checkout -b my_branch`
3. Push to your branch - `git push origin my_branch`
4. Create an [Issue][2] with a link to your branch
5. That's it!

Author
------
Richard Huang :: flyerhzm@gmail.com :: @flyerhzm

Copyright
---------
Copyright (c) 2010 Richard Huang. See LICENSE for details.

[0]: http://github.com/defunkt/resque
[1]: http://help.github.com/forking/
[2]: http://github.com/flyerhzm/resque-restriction/issues

