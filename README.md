# Restapi_featchdata
Featch data in php using rest api
<?php
$conn=mysqli_connect("localhost","root"," ","Restapi");

$request=$_SERVER['REQUEST_METHOD'];
$data=array();
switch ($request) {
	case 'GET':
		response(getdata());
		break;
	
	default:
		# code...
		break;
}
function getdata()
{
	global $conn;
	$query=mysqli_query($conn,'select * from rest');
	while($row=mysqli_fetch_assoc($query))
	{
       $data[]=array("id"=>$row['id'],"name"=>$row['name'],"age"=>$row['age']);
	}
	return $data;
}
function response($data)
{
	//json formet
  echo json_encode($data);
}


?>
