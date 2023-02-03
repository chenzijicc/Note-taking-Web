```sql
declare @str varchar(100)
set @str='6907376211129'  --要搜索的字符串

declare @s varchar(8000)
declare tb cursor local for
select s='if exists(select 1 from ['+b.name+'] where ['+a.name+'] like ''%'+@str+'%'')
 print ''所在的表及字段: ['+b.name+'].['+a.name+']'''
from syscolumns a join sysobjects b on a.id=b.id
where b.xtype='U' and a.status>=0
 and a.xusertype in(175,239,231,167)
open tb
fetch next from tb into @s
while @@fetch_status=0
begin
 exec(@s)
 fetch next from tb into @s
end
close tb
deallocate tb
```