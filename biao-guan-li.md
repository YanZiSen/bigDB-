点击数据库列表的任意一项即可切换为该数据库的表管理页面，相应的，数据库列表切换为对应数据库的数据表列表

* 创建数据表

  在数据表列表上面点击新建表库快捷键右侧会出现新建数据表页面，带星号输入框为必填项，其余为选填项，可以创建PARQUET和KUDU两种类型的表，通过切换类型实现。

  针对不同的场景，用户数据建模可以选择两种不同类型的表，一种是只读的parquet格式的表，另一种是支持读写的kudu表。

  * **Parquet表**：一种使用Parquet文件进行表数据存储的表。用户可以指定列名和列类型进行建模，为了提高查询性能，还支持使用特定的列进行分区。

    * 使用场景

      各种历史数据存储查询分析场景。在这种场景下，当前存储的数据不和表中的数据做任何ROLL-UP操作，直接存入parquet表 中，以便之后做离线分析和历史数据聚合查询。一个典型的例子是每小时、每天统计某媒体网站财经新闻的PV，通过插码采集用户访问某媒体网站的行为日志（包含新闻类别，新闻标题，时间，来源等明细信息），然后直接存入parquet表中，使用sql统计最近一天浏览财经新闻的次数有多少。

  * **Kudu表**：使用kudu进行存储的表。数据建模过程中，用户除了指定列名和列属性外，还必须指定主键，以及可选的压缩算法。支持Hash和Range两种分区方式，以及它们的混合形式。

    * 使用场景

      流数据存储，实时分析场景。由于kudu具有更高的写入性能，所以非常适合存储流数据，通过upsert操作还能和表中数据进行归并。一个典型的例子就是收集和更新网站用户信息。一个表中已有用户进行了手机号绑定，就需要将用户的手机号信息更新到表中，或者实时更新用户的最后访问时间等，以便于查看网站用户留存情况。

  * 创建表的输入规范

    * <a href="#keywords"></a><div id="keywords">保留字</div>
      
       **add  ,  column  ,  end  ,  ilike  ,  not  ,  rename  ,  tables  ,  symbol  ,  aggregate  ,  columns  ,  escaped  ,  in  ,  null  ,  replace  ,  tablesample  ,  all  ,  comment  ,  exists  ,  incremental  ,  nulls  ,  restrict  ,  tblproperties  ,  alter  ,  compression  ,  explain  ,  init_fn  ,  offset  ,  returns  ,  terminated  ,  analytic  ,  compute  ,  extended  ,  inner  ,  on  ,  revoke  ,  textfile  ,  and  ,  create  ,  external  ,  inpath  ,  or  ,  right  ,  then  ,  anti  ,  cross  ,  FALSE  ,  insert  ,  order  ,  rlike  ,  timestamp  ,  api_version  ,  current  ,  fields  ,  int  ,  outer  ,  role  ,  tinyint  ,  as  ,  data  ,  fileformat  ,  integer  ,  over  ,  roles  ,  to  ,  asc  ,  database  ,  finalize_fn  ,  intermediate  ,  overwrite  ,  row  ,  TRUE  ,  avro  ,  databases  ,  first  ,  interval  ,  parquet  ,  rows  ,  truncate  ,  between  ,  date  ,  float  ,  into  ,  parquetfile  ,  schema  ,  unbounded  ,  bigint  ,  datetime  ,  following  ,  invalidate  ,  partition  ,  schemas  ,  uncached  ,  binary  ,  decimal  ,  for  ,  iregexp  ,  partitioned  ,  select  ,  union  ,  blocksize  ,  default  ,  format  ,  is  ,  partitions  ,  semi  ,  update  ,  boolean  ,  delete  ,  formatted  ,  join  ,  table  ,  sequencefile  ,  update_fn  ,  by  ,  delimited  ,  from  ,  last  ,  preceding  ,  serdeproperties  ,  upsert  ,  cached  ,  desc  ,  full  ,  left  ,  prepare_fn  ,  serialize_fn  ,  use  ,  cascade  ,  describe  ,  function  ,  like  ,  produced  ,  set  ,  using  ,  case  ,  distinct  ,  functions  ,  limit  ,  purge  ,  show  ,  values  ,  cast  ,  div  ,  grant  ,  lines  ,  range  ,  smallint  ,  varchar  ,  change  ,  double  ,  group  ,  load  ,  rcfile  ,  stats  ,  view  ,  char  ,  drop  ,  hash  ,  location  ,  real  ,  stored  ,  when  ,  class  ,  else  ,  having  ,  merge_fn  ,  refresh  ,  straight_join  ,  where  ,  close_fn  ,  encoding  ,  if  ,  metadata  ,  regexp  ,  string  ,  with  ,  any  ,  current_date  ,  file  ,  offsets  ,  return  ,  unique  ,  authorization  ,  current_time  ,  fillfactor  ,  open  ,  revert  ,  unpivot  ,  backup  ,  current_timestamp  ,  for  ,  option  ,  rollback  ,  updatetext  ,  begin  ,  current_user  ,  foreign  ,  percent  ,  rowcount  ,  user  ,  break  ,  cursor  ,  freetext  ,  pivot  ,  rule  ,  varying  ,  browse  ,  dbcc  ,  goto  ,  plan  ,  save  ,  waitfor  ,  bulk  ,  deallocate  ,  holdlock  ,  precision  ,  securityaudit  ,  while  ,  cascade  ,  declare  ,  identity  ,  primary  ,  session_user  ,  within  ,  check  ,  default  ,  index  ,  print  ,  setuser  ,  writetext  ,  checkpoint  ,  deny  ,  intersect  ,  proc  ,  shutdown  ,  close  ,  disk  ,  key  ,  procedure  ,  some  ,  clustered  ,  distributed  ,  kill  ,  public  ,  statistics  ,  coalesce  ,  dump  ,  lineno  ,  raiserror  ,  system_user  ,  collate  ,  errlvl  ,  merge  ,  read  ,  textsize  ,  commit  ,  escape  ,  national  ,  readtext  ,  then  ,  constraint  ,  except  ,  nocheck  ,  reconfigure  ,  top  ,  contains  ,  exec  ,  nonclustered  ,  references  ,  tran  ,  continue  ,  execute  ,  nullif  ,  replication  ,  transaction  ,  convert  ,  exit  ,  of  ,  restore  ,  trigger  ,  current  ,  fetch  ,  off  ,  restrict  ,  try_convert**  
* 查看数据表详情

  在数据表列表项点击任意一项即可查看该数据表详情，可以查看该表每一列的类型，默认值，编码和压缩类型



