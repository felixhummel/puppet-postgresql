Install
=======
    # or some where else on the module path (see `puppet apply --configprint modulepath`)
    cd /etc/puppet/modules/
    sudo clone git://github.com/felixhummel/puppet-postgresql.git postgresql

Usage Example
=============
    # postgres-test.pp
    Exec { path => [ "/bin/", "/sbin/" , "/usr/bin/", "/usr/sbin/" ] }

    include postgresql

    postgresql::hba { "remove local peer access to all DBs":
      ensure   => absent,
      type     => 'local',
      database => 'all',
      user     => 'all',
      method   => 'peer',
      pgver    => '9.1',
    }

    postgresql::hba { "allow local md5 access to all DBs":
      ensure   => present,
      type     => 'local',
      database => 'all',
      user     => 'all',
      method   => 'md5',
      pgver    => '9.1',
    }

    postgresql::user { "test user":
      ensure => present,
      name => 'test',
      password => 'test',
      login => true,
    }

