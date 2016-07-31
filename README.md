function geraMusica(resultado, callback){
		var MusicasArray = resultado.split(";");
		var indice = Math.floor(Math.random() * MusicasArray.length);
		if( indice < 1 ){
			indice = 0;
		}else if(indice >= MusicasArray.length - 1){
			indice = MusicasArray.length - 2;
			
		}
		callback(MusicasArray[indice]);
}

// Função para adicionar vinheta na playlist(intercalar uma música)
// Função para adicionar vinheta na playlist(intercalar uma música)
function add_vinheta(pasta,porta) {
  
  var frequencia = parseInt(prompt("Informe a cada quantas músicas será adicionada o conteudo desta pasta\nExemplo: 5"));
  var frequencia2 = parseInt(prompt("Informe quantos conteudos da pasta seram adicionados:\nExemplo: 1"));
  
  var lista_musicas = document.getElementById("lista-musicas-playlist");
	
  var total_musicas = 0;
  var MusicasDaPasta;
  if(porta == "" || pasta == "") {
  alert("Erro! Tente novamente ou contate o suporte.");
  } else {
  var http = new Ajax();
  http.open("GET", "/admin/funcoes-ajax/carregar_musicas_pasta/"+porta+"/"+pasta , true);
  http.onreadystatechange = function() {
	
  if(http.readyState == 4) {
  
	resultado = http.responseText;
	MusicasDaPasta = resultado;
	
  var listafilhos = lista_musicas.getElementsByTagName("li");
	
  for(var i=frequencia; i<=listafilhos.length; i+=frequencia+1) {
  	for(var a=frequencia2; a<=frequencia2; a+=frequencia2+1) {
  	console.log("valor de i2:");
  	console.log(i);

		if(novo_id) {
		  var novo_id = (novo_id+1);
		} else {
		  var novo_id = (total_musicas+1);
		  
		}
			
		var nova_musica = document.createElement("li");
			
		nova_musica.setAttribute("id",novo_id);
		nova_musica.setAttribute("class","musica");
		
		var musica = [];
		geraMusica(MusicasDaPasta, function(x){
			musica = x;
		});
		var pathMusica = musica.split("|")[0];
		var nomeMusica = musica.split("|")[1];
	  
		nova_musica.innerHTML = "<input name='musicas_adicionadas[]' type='checkbox' value='"+pathMusica+"' style='display:none' checked /><img src='/img/playlist/music.png' border='0' align='absmiddle' />&nbsp;<font color=\"#B10002\">"+nomeMusica+"</font><a href='javascript:remover_musica(\""+novo_id+"\")' style='float:right;'><img src='/img/playlist/cancel-circle.png' width='16' height='16' alt='Remover' title='Remover' border='0' align='absmiddle' /></a>";
			
		if (i == listafilhos.length) {
		  lista_musicas.appendChild(nova_musica);
		} else {
		  lista_musicas.insertBefore(nova_musica, listafilhos[i]);
		}
		console.log("Valor listafilhos: ");
		console.log(listafilhos[i]);
		console.log("valor nova_musica:");
		console.log(nova_musica);

		quantidade_musicas_playlist();
		
		setListeners();
	
        }
      }

    }
  
  }
  http.send(null);
  delete http;
  }
 
}
