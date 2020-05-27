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
// All crud operations in php using restapi featch data , insert data , update data
<?php
$conn=mysqli_connect("localhost","root"," ","Restapi");

$request=$_SERVER['REQUEST_METHOD'];
$data=array();
switch ($request) {
	case 'GET':
		response(getdata());
		break;
	case 'POST':
		response(adddata());
		break;
	case 'PUT':
		response(updatedata());
		break;
	
	default:
		# code...
		break;
}
function getdata()
{
	global $conn;
	// featch single record from data base
	if($GET['id']){
		$id=$_GET['id'];
		$where="where id=".$id;
	}
	else
	{
		$id=0;
		$where="";
	}
	$query=mysqli_query($conn,"select * from rest".$where);
	while($row=mysqli_fetch_assoc($query))
	{
       $data[]=array("id"=>$row['id'],"name"=>$row['name'],"age"=>$row['age']);
	}
	return $data;
}
function adddata(){
global $conn=mysqli_query($conn,"insert into rest(name,age)values(" ".$POST['name'].",".$POST['age'])");
   if($query==true)
   {
   	$data[]=array("message"=>"success");
   }
   else
   {
   	$data[]=array("message"=>"failed");
   }
   return $data;
}

function updatedata(){
	global $conn;
	parse_str(file_get_content('php://input'),$_PUT);
	if($GET['id']){
		$id=$_GET['id'];
		$where="where id=".$id;
	}
	else
	{
		$id=0;
		$where="";
	}

	$query=mysqli_query($conn,"update rest set name'".$_PUT['name'].'" age'".$_PUT['age']."'.$where);

   if($query==true)
   {
   	$data[]=array("message"=>"update");
   }
   else
   {
   	$data[]=array("message"=>"failed");
   }
   return $data;


}



function response($data)
{
	//json formet
  echo json_encode($data);
}


?>
