---
published: true
---
## Learn From Online Resource
* Learning from [Simplified Coding](https://www.simplifiedcoding.net/firebase-cloud-messaging-android/)
* It's really a very nice source of learning codes, highly recommended.



## Update To My Own Version

* I found there would be an issue when the server doesn't support mysqlnd driver, so it would require to replace $stmt->get_result() with $stmt->bind_result() which is available.
* Update the php file **Config.php** with the following codes.


```php
<?php 
	define('DB_USERNAME','MYSQL_USER'); 	// Customize this
	define('DB_PASSWORD','PASSWORD');		// Customize this
	define('DB_NAME','MYSQL_DATABASE');		// Customize this
	define('DB_HOST','localhost');	
	
	//defined a new constant for firebase api key
	define('FIREBASE_API_KEY', 'AIzaSyCaxKZycSRolmrAiFCwh5_6MJXKGl9PQ0g');
?>
```


* Update the php file **DbOperation.php** with the following codes.


```php
<?php
 
class DbOperation
{
    //Database connection link
    private $con;
 
    //Class constructor
    function __construct()
    {
        //Getting the DbConnect.php file
        require_once dirname(__FILE__) . '/DbConnect.php';
 
        //Creating a DbConnect object to connect to the database
        $db = new DbConnect();
 
        //Initializing our connection link of this class
        //by calling the method connect of DbConnect class
        $this->con = $db->connect();
    }
 
    //storing token in database 
    public function registerDevice($email,$token){
        if(!$this->isEmailExist($email)){
            $stmt = $this->con->prepare("INSERT INTO devices (email, token) VALUES (?,?) ");
            $stmt->bind_param("ss",$email,$token);
            if($stmt->execute())
                return 0; //return 0 means success
            return 1; //return 1 means failure
        }else{
            return 2; //returning 2 means email already exist
        }
    }
 
    //the method will check if email already exist 
    private function isEmailexist($email){
        $stmt = $this->con->prepare("SELECT id FROM devices WHERE email = ?");
        $stmt->bind_param("s",$email);
        $stmt->execute();
        $stmt->store_result();
        $num_rows = $stmt->num_rows;
        $stmt->close();
        return $num_rows > 0;
    }
 
    //getting all tokens to send push to all devices
    public function getAllTokens(){
        $stmt = $this->con->prepare("SELECT token FROM devices");
        if ($stmt->execute()) {
		//	echo "success<br>";
		}
		//else echo "failure<br>";
		
        $stmt->store_result();
		$stmt->bind_result($token);
		//echo $stmt->num_rows . "<br>";
			
		$tokens = array();
		while($stmt->fetch()) {
			$tmp = array();
			$tmp["token"] = $token;
			array_push($tokens, $tmp["token"]);
			
			//echo $token.'<br>';
		}
		
		$stmt->free_result();
		$stmt->close();
		return $tokens;
    }
 
    //getting a specified token to send push to selected device
    public function getTokenByEmail($email){
        $stmt = $this->con->prepare("SELECT token FROM devices WHERE email = ?");
        $stmt->bind_param("s",$email);
        if ($stmt->execute()) {
		//	echo "success<br>";
		}
		//else echo "failure<br>";
        //$result = $stmt->get_result()->fetch_assoc();
        //return array($result['token']);   
		
		$stmt->store_result();
		$stmt->bind_result($token);
		//echo $stmt->num_rows . "<br>";
			
		$tokens = array();
		while($stmt->fetch()) {
			$tmp = array();
			$tmp["token"] = $token;
			array_push($tokens, $tmp);
			
			//echo $token.'<br>';
		}
		
		$stmt->free_result();
		$stmt->close();
		//echo "token:".$token."<br>";
		return $token;
    }
	
	public function getAllDevices(){
		$stmt = $this->con->prepare("SELECT id, email, token FROM devices"); // WHERE id = 1 cause empty result
		//$stmt->bind_param("i", $id);
		//$stmt->bind_param("s", $email);
		//$stmt->bind_param("s", $token);
		if ($stmt->execute()) {
		//	echo "success<br>";
		}
		//else echo "failure<br>";
		
		$stmt->store_result();
		$stmt->bind_result($id, $email, $token);
		//echo $stmt->num_rows . "<br>";
			
		$devices = array();
		while($stmt->fetch()) {
			$tmp = array();
			$tmp["id"] = $id;
			$tmp["email"] = $email;
			$tmp["token"] = $token;
			array_push($devices, $tmp);
			
			//echo $id.' '.$email.' '.$token.'<br>';
		}
		
		$stmt->free_result();
		$stmt->close();
		return $devices;
	}
}

?>
```
