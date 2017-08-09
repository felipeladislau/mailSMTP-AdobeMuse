# mailSMTP-AdobeMuse
Ajuste para scripts de envio de e-mail do Adobe Muse para enviar mensagens com autenticação SMTP

Para utilizar você deve enviar para a pasta "scripts" a parta "requires" que contem as classes necessárias para rodar o SMTP.

Em seguida abra o script "process.php" e busque pela tag @mail(...), esta tag faz o envio do e-mail e nela você pode ver as variáveis que possuem os parâmetros necessários para o envio, vamos comentar esta tag e utilizar as variáveis para o SMTP.

Depois disto você deve colar o seguinte trecho de código abaixo da tag comentada:

  <?php
  // Tag antiga comentada
	// $sent = @mail($to, $subject, $message, $headers);

	/************************************************************************/
  // Início do script

	require_once('requires/class.phpmailer.php');
		 
	$mailer = new PHPMailer();
	$mailer->IsSMTP();
	$mailer->SMTPDebug = 1;
	$mailer->Port = 25; //Indica a porta de conexão para a saída de e-mails. Utilize obrigatoriamente a porta 587.
		 
	$mailer->Host = 'localhost'; //Onde em 'servidor_de_saida' deve ser alterado por um dos hosts abaixo:
	//Para cPanel: 'localhost';
	//Para Plesk 11 / 11.5: 'smtp.dominio.com.br';
		 
	//Descomente a linha abaixo caso revenda seja 'Plesk 11.5 Linux'
	//$mailer->SMTPSecure = 'tls';
		 
	$mailer->SMTPAuth = true; //Define se haverá ou não autenticação no SMTP
	$mailer->Username = 'nao-responda@seusite.com.br'; //Informe o e-mai o completo
	$mailer->Password = 'senhadefinidadoemail'; //Senha da caixa postal
	$mailer->FromName = 'Seu Site - Não responda'; //Nome que será exibido para o destinatário
	$mailer->From = 'nao-responda@seusite.com.br'; //Obrigatório ser a mesma caixa postal indicada em "username"
	$mailer->AddAddress($to); //Destinatários
	$mailer->Subject = $subject;
	$mailer->Body = $message;

  // Este ajuste permite que as verificações de envio e falha continuem ocorrendo normalmente.
	if(!$mailer->Send())
	{
		$sent = false;
	}else{
		$sent = true;
	}
	?>
	/************************************************************************/


Espero que gostem e resolvam este problema com isto.

Abraços :)
