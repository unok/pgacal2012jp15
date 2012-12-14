.. coding:sjis

==========================================================
�����̃o�[�W�������C���X�g�[����, ���R���݂ɑ��낤
==========================================================

:Author: sakamotomsh
:Date: 2012-12-15

.. sectnum::

�͂��߂�
----------

�{�L���� `PostgreSQL Advent Calender 2012`_ ��12/15 �p�̋L���ł��B
����github��̃��|�W�g�� `pgacal2012jp15`_ ���g��,
github:pages�̋@�\�Ńz�X�e�B���O���Ă��܂��B

.. _`PostgreSQL Advent Calender 2012`: http://atnd.org/events/34176
.. _`pgacal2012jp15`: https://github.com/sakamotomsh/pgacal2012jp15

�ڕW
---------

- ��̃T�[�o��,
- �����̃o�[�W������PostgreSQL���C���X�g�[����,
- ���R���݂ɐ؂�ւ��Ďg�����@���Љ�/��Ă��܂��B

�C���g���_�N�V����
--------------------

���͖^�V�X�e����Ђ�PostgreSQL�̖₢���킹�Ɩ������Ă��܂��B
�₢���킹�Ɩ��ł̓X�s�[�h�����ł��B
�₢���킹���󂯕t���Ă�����\�z����, ����͂�����, �񓚂�����....
����Ȃ��Ƃ�����Ă���Ǝ��Ԃ������炠���Ă�����܂���B

����Ȓ�, ���⓯���̑����͊��\�z�̎������Ȃǂ̃e�N�j�b�N�������Ă��܂��B  
�����͂��̂����̈�Ƃ���, �����g���Ă��� **�u��̃T�[�o�ɕ�����PostgreSQL
���C���X�g�[����, ���R���݂Ɋ���؂�ւ�����@�v** ���Љ�܂��B

���p��Ƃ��� **�u�������v���P�[�V�����N���X�^���ƂĂ��ɊȒP�ɂł��邱�Ɓv** 
���f�����X�g���[�V�������܂��B

*���L*: �{�L���Ɣ��Ɏ����ړI�̃\�t�g�E�F�A�Ƃ��� pgvm_ ������܂��B �F����l���邱�Ƃ͈ꏏ�ł���..

.. _pgvm: https://github.com/guedes/pgvm


�Z�p�I�ȗv�f
----------------

- �\�[�X�R�[�h�̓���
    PostgreSQL�� `git�Ń\�[�X�R�[�h�Ǘ�`_ ����Ă��܂��B �����Ċe�o�[�W�����͖�����
    �����K��Ɋ�Â����^�O�����t�^����Ă��܂��B  ���̂���, clone�������[�J����
    git���|�W�g������ **�u�V�X�e�}�e�B�b�N�Ɂv** �C�ӂ̃o�[�W�����̃\�[�X�R�[�h�����ł��܂��B

- �R���p�C��/�C���X�g�[��
    configure����prefix�I�v�V�����ŃC���X�g�[�����t�^�����, 
    ��̃T�[�o�ɂ�����ł�PostgreSQL���C���X�g�[�����邱�Ƃ��ł��܂��B
    ���̍ۂ�--enable-debug�Ȃǉ�͂ɖ𗧂I�v�V���������邱�Ƃ��ł��܂��B

- ���̕���/�؂�ւ�
    PostgreSQL�̓C���X�g�[�����������ł͎g���܂���B
    ��������PostgreSQL�ǂ����̎g�p����|�[�g�ԍ������Ԃ�Ȃ��悤�ɂ�����
    �K�؂�PATH�ݒ�����ĖړI�̃o�[�W������pg_ctl���Ăяo������,
    initdb����f�[�^�x�[�X�̈���m�ۂ����肷��K�v������܂��B

    ��ʓI�Ȍ������������ **�u���̐؂�ւ��v** ���K�v�ƂȂ�܂��B
    python��virtualenv�ł���activate, node.js��nvm�ɂ�����use�ɑ�������@�\�ł��B 
    PostgreSQL�̏ꍇ, **�u��{�I�Ɋ��ϐ���ݒ肷�邾���v** �Ŋ��𕪗��ł��܂��B

    - PATH���ϐ�: ����Ώۂ̃o�[�W������pg_ctl/psql����������悤�ɐݒ�
    - PGDATA���ϐ�: �o�[�W�������ƂɈႤ�f�[�^�̈��ݒ�
    - PGPORT���ϐ�: ����T�[�o�œ��삳�����ۂɃ|�[�g�ԍ��̏d�������Ȃ��悤�ɐ�
      ��(�{����postgresql.conf��port�Őݒ肷�ׂ��ł���, pg_ctl�����łȂ�
      psql�Ȃǂ̃N���C�A���g�A�v���P�[�V�������ÖٓI�ɐڑ�����|�[�g�ԍ���
      �ݒ�ł���Ƃ��������b�g�̂��ߊ��ϐ��Őݒ肵�܂�)

    �����̊��ϐ����Z�b�g����bash�� `exec`_ ���Ă�����v���O���������Ƃ悳�����ł��B
    ���ł�PS1���ϐ����������Ă�����, ���݂ǂ̃o�[�W�������g���Ă��邩���킩��₷���\��
    ����̂��悢�ł��傤�B

���������o�܂�, �����쐬�����̂���̃v���O���� `pginstall`_ �� `pgbash`_ �ł��B
�O�҂̓C���X�g�[�����ȗ�����, ��҂͊��ؑւ��ȗ������܂��B

�ȉ��������L�ڂ��܂���, �Z�p�I�ȕ����͈ȏ�ŃJ�o�[�����̂�,
���̐�͋����̂�����̂ݓǂݐi�߂Ă��������B
�܂�, �����Ȃ�̃c�[�������삵�Ă��ʔ����Ǝv���܂��B
���Ѓ`�������W���Ă݂Ă��������B

.. _`git�Ń\�[�X�R�[�h�Ǘ�`: http://git.postgresql.org/gitweb/?p=postgresql.git;a=summary
.. _`exec`: http://linuxjm.sourceforge.jp/html/LDP_man-pages/man3/exec.3.html

pginstall: �C���X�g�[���ȗ����X�N���v�g 
-------------------------------------------------

�X�N���v�g�̑S�̂� `pginstall`_ �ɋL�ڂ��܂����B 
python�ō����100�s������Ƃ̃X�N���v�g�ł��B 
/usr/bin �Ȃ�PATH���ʂ��Ă���ꏊ�ɔz�u�����
�{���ɊȒP��PostgreSQL���C���X�g�[���ł��܂��B�g�����͂����ł�

.. code:: bash

    $ pginstall 8.4.12

.. _`pginstall`: https://github.com/sakamotomsh/pgacal2012jp15/blob/master/pginstall
.. _`pgbash`: https://github.com/sakamotomsh/pgacal2012jp15/blob/master/pgbash

���œ����R�}���h�̓�����������Ă݂܂��傤�B

.. code:: bash

    #�\�[�X�R�[�h�̒��o
    cd /home/pgacal2012jp15/.pgbash/repo
    mkdir /home/pgacal2012jp15/.pgbash/src/pgsql-8.4.12
    git archive REL8_4_12 | tar -x -C /home/pgacal2012jp15/.pgbash/src/pgsql-8.4.12
    
    #�R���p�C���ƃC���X�g�[��
    cd /home/pgacal2012jp15/.pgbash/src/pgsql-8.4.12
    ./configure --prefix=/home/pgacal2012jp15/.pgbash/bin/pgsql-8.4.12 --enable-debug
    make; make install
    cd contrib; make ; make install

�܂�git archive�R�}���h�ŃC���X�g�[���Ώۂ̃o�[�W�����̃\�[�X�R�[�h�𔲂��o��
��, configure����ۂ�prefix���w�肵�ăC���X�g�[�����邾���̊ȒP�ȍ�Ƃł��B

�������⑫�ł��BPostgreSQL�̃��|�W�g���Ƃ��� $HOME/.pgbash/repo ���g���܂��B
�Ȃ����git clone����悤�w������܂��B�\�[�X�R�[�h, �C���X�g�[���o�C�i���Ȃ�
�S�Ẵf�[�^�� $HOME/.pgbash �z���ɒu����܂��B

���̂悤�Ɉ��̃}�V���ɕ�����PostgreSQL���C���X�g�[������̂͂ƂĂ��ȒP�ł��B
�V�X�e�}�e�B�b�N��PostgreSQL���C���X�g�[���ł���悤�ɂȂ��,
�u������ƕʃo�[�W�����œ������Ă݂邩�v�Ǝv����悤�ɂȂ�܂��B
**���̂悤�ȐS����ԂɂȂ�̂���Ԃ̌��\�ł�**.�݂Ȃ�������Ў����Ă݂ĉ������B


pgbash: ���ؑփV�F��
-------------------------

�X�N���v�g�̑S�̂� `pgbash`_ �ɋL�ڂ��܂����B 
���؂�ւ��Ɋւ��Ă�, ��������ׂ��@�\����������܂��B

- �@�\A: �ǂ̃o�[�W�������g���邩�ꗗ������/�ǂ̃o�[�W�������N�����Ă��邩��\������
- �@�\B: ����؂�ւ���(bash��exec����)

�@�\A�͈ȉ��̂悤�ɂ����܂�::

    $ pgbash -l
    [ ] pgsql-8.4.10
    [*] pgsql-8.4.12 (port=18412,port=28412)
    [ ] pgsql-8.4.5
    [ ] pgsql-9.0.2
    [*] pgsql-9.0.7 (port=19007)
    [ ] pgsql-9.1.5
    [ ] pgsql-9.2.0
    [ ] pgsql-9.2.1


���̊��ł�, ���\���낢��ȃo�[�W�������C���X�g�[������Ă��邱�Ƃ��킩��܂��B
������[\*]�͌��݂��̃o�[�W�����̃T�[�o���N�����ł��邱�Ƃ�����킵�܂��B
Ver8.4.12�̃C���X�^���X��2��, Ver9.0.7�̃C���X�^���X��1�������Ă���悤�ł��B
���͂��̕\��������̂���ςł���. lsof�R�}���h��PostgreSQL�̃h���C���\�P�b�g�ꗗ��
�����ێ����Ă���PID�̑Ή�����_��, ps�R�}���h��postmaster�̃v���O�����p�X����
�ǂ̃o�[�W�������ǂ̃|�[�g�œ��삵�Ă���̂��𐄒肵�Ă��܂��B

�@�\B��, ��قǏq�ׂ��悤��, ���ϐ���ݒ肵��bash�𗧂��グ�邾����
�v���O�����ł��B 

Ver9.2.1�𗧂��グ�Ă݂܂�::

    $ pgbash pgsql-9.2.1 
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ pg_ctl start
    server starting
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ pgbash -l
    [ ] pgsql-8.4.10
    [*] pgsql-8.4.12 (port=18412,port=28412)
    [ ] pgsql-8.4.5
    [ ] pgsql-9.0.2
    [*] pgsql-9.0.7 (port=19007)
    [ ] pgsql-9.1.5
    [ ] pgsql-9.2.0
    [*] pgsql-9.2.1 (port=19201) ���������N������

���̂悤�ɐV����bash�������オ��, pg_ctl �Ȃǂ��o�[�W�������ӎ������ɑł��Ƃ�
�ł��܂��B���ۂɐ������p�X���ݒ肳��Ă��邩�H�����m�F���Ă݂܂��傤::

    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ psql -c "select version()"
                                                       version
    --------------------------------------------------------------------------------------------------------------
     PostgreSQL 9.2.1 on x86_64-unknown-linux-gnu, compiled by gcc (GCC) 4.4.6 20120305 (Red Hat 4.4.6-4), 64-bit
    (1 row)
    
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ which psql
    ~/.pgbash/bin/pgsql-9.2.1/bin/psql
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ echo $PGDATA $PGPORT
    /home/pgacal2012jp15/.pgbash/data/pgsql-9.2.1-1 19201

���̂悤�ɁA�o�[�W������؂�ւ���PostgreSQL���v�����܂܂Ɉ����܂��B


�~�b�V����: �������v���P�[�V�����N���X�^���\�z����
----------------------------------------------------------

�ŋ߃����[�X���ꂽPostgreSQL�� 9.2.2 ��V�K�ɃC���X�g�[������,
�������v���P�[�V�������N���X�^��g��ł݂܂��傤�B 
�Ƃ����Ă�, �ȉ������҂؂��邾���ł��B
��t�̃R�[�q�[�����ގ��Ԃ��Ȃ�, �N���X�^���\�z�ł��܂���

.. code:: bash
    
    TARGET_VERSION=9.2.2
    ENV_ID=pgsql-$TARGET_VERSION

    #Install ##################################################################
    yes | pginstall $TARGET_VERSION

    #Setup Master##############################################################
    pgbash $ENV_ID 1
    rm -rf $PGDATA
    initdb --no-locale -U postgres
    cat << EOF >> $PGDATA/postgresql.conf
    wal_level = hot_standby
    max_wal_senders = 3
    hot_standby = on
    EOF
    cat << EOF >> $PGDATA/pg_hba.conf
    host replication postgres 0.0.0.0/0 trust
    host replication postgres ::1/0 trust
    EOF
    pg_ctl -w start
    pgbench -i
    exit
    
    #Setup Standby############################################################
    pgbash $ENV_ID 2
    pg_basebackup -x -c fast -D $PGDATA -h localhost -p `expr $PGPORT - 10000`
    cat << EOF >> $PGDATA/recovery.conf
    standby_mode = 'on'
    primary_conninfo = 'host=localhost port=`expr $PGPORT - 10000` user=postgres application_name=sby01'
    EOF
    pg_ctl -w start
    exit

    #Start Replication #######################################################
    pgbash $ENV_ID 1
    echo "synchronous_standby_names = '*'" >> $PGDATA/postgresql.conf
    pg_ctl -w restart
    exit

�m���߂Ă݂܂�::

    $ pgbash -l
    [ ] pgsql-8.4.10
    [*] pgsql-8.4.12 (port=18412,port=28412)
    [ ] pgsql-8.4.5
    [ ] pgsql-9.0.2
    [*] pgsql-9.0.7 (port=19007)
    [ ] pgsql-9.1.5
    [ ] pgsql-9.2.0
    [*] pgsql-9.2.1 (port=19201)
    [*] pgsql-9.2.2 (port=19202,port=29202)
    
    $ pgbash pgsql-9.2.2
    (pgsql-9.2.2-1)[pgacal2012jp15@~]$ psql -xc "select * from pg_stat_replication"
    -[ RECORD 1 ]----+------------------------------
    pid              | 28019
    usesysid         | 10
    usename          | postgres
    application_name | sby01
    client_addr      | ::1
    client_hostname  |
    client_port      | 43608
    backend_start    | 2012-12-12 00:08:13.220873+09
    state            | streaming
    sent_location    | 0/4000080
    write_location   | 0/4000080
    flush_location   | 0/4000080
    replay_location  | 0/4000080
    sync_priority    | 1
    sync_state       | sync

�Ō��
----------
���[�`�����^��/���������邱�Ƃł�����ɂ�Ƃ肪���܂�܂��B
���܂ꂽ��Ƃ��, �^�̈Ӗ��Ő��Y�������߂��邱�ƂɐS���g���܂��傤�B

����12/16��yohgaki����ł�.


.. vim: tw=80 :
