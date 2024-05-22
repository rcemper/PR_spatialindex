# How to use

Import SpatialIndex package.
Define index in class as follows (you can use any index, properties name):

`Index x1f on (Latitude,Longitude) As SpatialIndex.Index;`

See sample class SpatialIndex.Test

Load data with

   do ##class(SpatialIndex.Test).load("/tmp/Rucut.txt")

Then you can query table with defined index.
Two types of queries are implemented:
window (rectangle) and radius (ellipse).

For example:

	SELECT *
	FROM SpatialIndex.Test
	WHERE %ID %FIND search_index(x1F,'window','minx=56,miny=56,maxx=57,maxy=57')

or

	SELECT *
	FROM SpatialIndex.Test
	WHERE  %ID %FIND search_index(x1F,'radius','x=55,y=55,radius=2')
	and name %StartsWith 'Z'

or

	SELECT *
	FROM SpatialIndex.Test
	WHERE  %ID %FIND search_index(x1F,'radius','x=55,y=55,radiusX=2,radiusY=2')
	and name %StartsWith 'Z'

## Docker    

### Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.
### Installation
Clone/git pull the repo into any local directory
```
$ git clone https://github.com/rcemper/PR_System-Alerts.git
```
to build and start the container run     
```
$ docker compose up -d && docker compose logs -f
```
A deom Task is prepared. It's named **docker**    
http://localhost:42773/csp/sys/op/%25CSP.UI.Portal.TaskInfo.zen?$ID1=1000      
It is ready for you to adjust it to your needs.    

To open IRIS Terminal do:   
```
$ docker-compose exec iris iris session iris 
USER>
```
or using **WebTerminal**     
http://localhost:42773/terminal/      

To access IRIS System Management Portal   
http://localhost:42773/csp/sys/UtilHome.csp    

### Testing   
The easiest way is to enter a terminal session    
and start SQL Shell with its alias  **:sql**    
and execute the examples in multiline mode   
	
	USER>:sql
	SQL Command Line Shell
	----------------------------------------------------
	
	The command prefix is currently set to: <<nothing>>.
	Enter <command>, 'q' to quit, '?' for help.
	[SQL]USER>>  << entering multiline statement mode, 'GO' to execute >>
        1>>SELECT *
        2>>FROM SpatialIndex.Test
        3>>WHERE  %ID %FIND search_index(x1F,'radius','x=55,y=55,radiusX=2,radiusY=2')
        4>>and name %StartsWith 'Z'
        5>>
        5>>go
		
1.      SELECT *
        FROM SpatialIndex.Test
        WHERE  %ID %FIND search_index(x1F,'radius','x=55,y=55,radiusX=2,radiusY=2')
        and name %StartsWith 'Z'

| ID | Latitude | Longitude | Name |
| -- | -- | -- | -- |
| 1446 | 56.6 | 54.05 | Zyablovo |
| 1517 | 56.5461 | 56.1358 | Zverevo |
| 1551 | 55.88074 | 53.2886 | Zuyevy Klyuchi |
| 1571 | 55.88191 | 53.22122 | Zuyevo |
| 1572 | 55.26306 | 55.81972 | Zuyevo |
 
	-------
