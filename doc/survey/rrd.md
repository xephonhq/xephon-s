# Round Robin Database

- rrdtool https://github.com/oetiker/rrdtool-1.x
  - http://oss.oetiker.ch/rrdtool/doc/rrdtool.en.html
- http://www.loriotpro.com/Products/On-line_Documentation_V5/LoriotProDoc_EN/V22-RRD_Collector_RRD_Manager/V22-A1_Introduction_RRD_EN.htm
- http://cuddletech.com/articles/rrd/ar01s02.html

## Meta

- On Disk Size: fixed
- Time Interval: constant interval

## Terms

- RRD: Round Robin Database
- RRA: Round Robin Archive
- CF: Consolidation functions (MAX, MIN, AVG, LAST)
  - [ ] I think is called `roll-up` or `aggregation` in other TSDBs

## Architecture

- **One RRD can contains multiple RRA**
  - [ ] If I have 3 RRA with interval of 1 hour, 1 minutes and 1 second, when and where is the consolidation function executed? Is there any requirement
  for the size of multiple RRAs, i.e. the RRA using one second should be larger than 60 so the values to be dropped can be consolidated and put into another more coarse grained RRA.
- Data values of the same consolidation setup are stored into Round Robin Archives (RRA)
- 'Unknown' is used when data point is not available when they should be
