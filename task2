<?php
if( isset( $_GET[ 'Login' ] ) ) {
	// CWE-20: Improper Input Validation
	//      Необходимо производить проверку username и password, например isset ($_POST["username"], ["password"]),   иcпользование POST во избежании слива паролей
	$user = $_GET[ 'username' ];
	$pass = $_GET[ 'password' ];

    	// CWE-327: Use of a Broken or Risky Cryptographic Algorithm
	// CWE-328: Use of Weak Hash
	// Слабый и старый криптографический алгоритм md5 стоит заменить например на sha512 или  password_hash в PHP, с алгоритмом хеширования, таким как bcrypt
	$pass = md5( $pass );

	// CWE-89 : Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')
	//      Необходимо использовать метод mysql_real_escape_string()
	//      Использование параметризированных запросов

	// CWE-306: Missing Authentication for Critical Function
	// Необходимо, что бы запрос к бд делал пользователь только с правами чтения
	// CWE-307: Improper Restriction of Excessive Authentication Attempts
	// Необходимо ограничить количество запросов (например, капча)
	// CWE-799: Improper Control of Interaction Frequency
	// Необходимо ограничить количество попыток аунтефикации
	$query  = "SELECT * FROM `users` WHERE user = '$user' AND password = '$pass';";
	$result = mysqli_query($GLOBALS["___mysqli_ston"],  $query ) or die( '<pre>' . ((is_object($GLOBALS["___mysqli_ston"])) ? mysqli_error($GLOBALS["___mysqli_ston"]) : (($___mysqli_res = mysqli_connect_error()) ? $___mysqli_res : false)) . '</pre>' );

	if( $result && mysqli_num_rows( $result ) == 1 ) {
		$row    = mysqli_fetch_assoc( $result );
		$avatar = $row["avatar"];
		$html .= "<p>Welcome to the password protected area {$user}</p>";
		$html .= "<img src=\"{$avatar}\" />";
	}
	else {
		$html .= "<pre><br />Username and/or password incorrect.</pre>";
	}
	((is_null($___mysqli_res = mysqli_close($GLOBALS["___mysqli_ston"]))) ? false : $___mysqli_res);
}
?>
