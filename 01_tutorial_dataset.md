### The Tutorial Data Set
https://denbi-nanopore-training-course.readthedocs.io/en/latest/data.html

Login as root
```
sudo su
```
Download the data
```
wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/nanopore_course_data/Data_Group1.tar.gz &>/dev/null &
wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/nanopore_course_data/Results_Group1.tar.gz &>/dev/null &
wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/nanopore_course_data/Data_Group2.tar.gz &>/dev/null &
wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/nanopore_course_data/Results_Group2.tar.gz &>/dev/null &
```

Unpack the files
```
tar -xzvf Data_Group1.tar.gz &>/dev/null &
tar -xzvf Results_Group1.tar.gz &>/dev/null &
tar -xzvf Data_Group2.tar.gz &>/dev/null &
tar -xzvf Results_Group2.tar.gz &>/dev/null &

```
and remove the tar archives:
```
rm Data_Group1.tar.gz
rm Results_Group1.tar.gz
rm Data_Group2.tar.gz
rm Results_Group2.tar.gz
```
Have a short look, on what is contained within the data directory:
```
ls -l ~/workdir/data/
```
