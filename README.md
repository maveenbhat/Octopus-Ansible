# Octopus-Ansible

I was working with a poll application, the poll application starts with a Python Flask web client that gathers the votes, and then pushes them into a Redis queue. Afterwards, the Java worker consumes the votes stored in the Redis queue, and pushes them into a PostgreSQL database. Finally, the Node.js web client fetches the votes from the PostgreSQL database and displays the results.

I deployed the poll application onto 5 different machines, without using containers, by using Ansible.

It consists of 6 roles:-

-->base
This role is associated to all machines.
• Installs usefulpackages (suchasGit) using apt.
• Configures instance.

-->redis
• Installs Redis.
• Sets up Redis.

-->postgresql
• Installs PostgreSQL 12 and psql tool.
• Creates a user paul with the password democracyIsFragile and limited permissions. 
• Creates the schema of the database paul.

-->poll
• Uploads poll service.
• Installs dependencies.
• Runs the poll web client.

-->worker
• Uploads worker service.
• Installs dependencies. 
• Builds the worker.
• Runs the worker.

-->result
• Uploads result service.
• Installs dependencies.
• Runs the result web client.

All services are managed by systemd and start automatically on boot.
