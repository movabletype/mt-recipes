## Description

Generate a Movable Type entry's basename from the title, such as when you retrieve entries directly from the database and want to create the permalink.

## Details

function makeFilename($name) {
  $name = strtolower($name);
  $name = preg_replace("/[^a-z^0-9^\s^-]{1}/","",$name);
  $name = preg_replace("/\s+/","_",$name);
  $name = substr($name,0,20);
  return $name;
}
