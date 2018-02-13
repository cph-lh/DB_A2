## **Running the program**
You need to install several things to run the program:

**1) Docker**

You can use Docker to run the program, but note that it is only necessary, but if you **DON'T** have a virtual machine running!

If you want to use Docker though, you need to set up a container first.
You can set up a Docker container by running the following command:`$ docker run --rm -v $(pwd)/data:/data/db --publish=27017:27017 --name dbms -d mongo`

This will give you an ID for the container. Use this ID to run the following: `$ docker exec -it YOUR_ID bash`

**Examble:** `$ docker exec -it 8f367e3a857e bash`

If it says you already have a contained with that ID, you can run `$ docker ps` to retrieve the ID.
#

**2) wget and unzip**

Then you need to have both 'wget' and 'unzip' installed. If you're using the Docker container, you need to run the following instructions inside the container.

- First update apt-get: `$ apt-get update`
- Then install wget and unzip with `$ apt-get install -y wget` and `$ apt-get install -y unzip`
- Use wget to download a zip file containing the data: 
```
$ wget http://cs.stanford.edu/people/alecmgo/trainingandtestdata.zip
```
- Unzip the file: `$ unzip trainingandtestdata.zip`
- Add keys to the file: 
```
$ sed -i '1s;^;polarity,id,date,query,user,text\n;' training.1600000.processed.noemoticon.csv
```
- Add documents to the database:
```
$mongoimport --drop --db social_net --collection tweets --type csv --headerline --file training.1600000.processed.noemoticon.csv
```


**NOTE:** If you're on a Mac and decide not to use the Docker container, you can't use `apt-get` to install wget and unzip. There are many other ways of doing this, but I personally used Homebrew by running `$ brew install wget` and `$ brew install unzip`.
#

**3) python and pymongo**

You also need to have python and pymongo installed - these can easily be installed with pip.

- Install pip: `$ sudo apt-get install python-pip python-dev build-essential`
- Install python:
```
$ sudo apt-get update
$ sudo apt-get -y upgrade
$ python3 -v
```
- Install pymongo: `$ python -m pip install pymongo`

After this, you can download the `mongodb.py` from the GitHub repository and then run the file by typing `$ python mongodb.py`.

**NOTE:** If you're on a Mac, you can't use `apt-get` to install pip. Instead simply just use `$ sudo easy_install pip`. To install python on your Mac you can either download and install the package from their website (python.org) or use Homebrew by typing `$ brew install python`.

## **Results**

I had 1287 errors, when loading the csv into mongodb. So that may change our results.
How many Twitter users are in the database? 659178

Which Twitter users link the most to other Twitter users? (Provide the top ten.) [{'_id': 'lost_dog', 'text': 549}, {'_id': 'tweetpet', 'text': 310}, {'_id': 'VioletsCRUK', 'text': 251}, {'_id': 'what_bugs_u', 'text': 246}, {'_id': 'tsarnick', 'text': 245}, {'_id': 'SallytheShizzle', 'text': 229}, {'_id': 'mcraddictal', 'text': 217}, {'_id': 'Karen230683', 'text': 216}, {'_id': 'keza34', 'text': 211}, {'_id': 'DarkPiano', 'text': 202}]

Who is are the most mentioned Twitter users? (Provide the top five.) [{'_id': '@mileycyrus', 'count': 4310}, {'_id': '@tommcfly', 'count': 3836}, {'_id': '@ddlovato', 'count': 3349}, {'_id': '@Jonasbrothers', 'count': 1263}, {'_id': '@DavidArchie', 'count': 1221}]

Who are the most active Twitter users (top ten)? [{'_id': 'lost_dog', 'count': 549}, {'_id': 'webwoke', 'count': 345}, {'_id': 'tweetpet', 'count': 310}, {'_id': 'SallytheShizzle', 'count': 281}, {'_id': 'VioletsCRUK', 'count': 279}, {'_id': 'mcraddictal', 'count': 276}, {'_id': 'tsarnick', 'count': 248}, {'_id': 'what_bugs_u', 'count': 246}, {'_id': 'Karen230683', 'count': 238}, {'_id': 'DarkPiano', 'count': 236}]

Who are the five most grumpy (most negative tweets). (Provide five users for each group) [{'_id': 'lost_dog', 'count': 549}, {'_id': 'tweetpet', 'count': 310}, {'_id': 'webwoke', 'count': 264}, {'_id': 'wowlew', 'count': 210}, {'_id': 'mcraddictal', 'count': 210}]

Who are the five the most happy (most positive tweets)? [{'_id': 'what_bugs_u', 'count': 246}, {'_id': 'DarkPiano', 'count': 231}, {'_id': 'VioletsCRUK', 'count': 218}, {'_id': 'tsarnick', 'count': 212}, {'_id': 'keza34', 'count': 211}]
