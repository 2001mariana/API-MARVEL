# API-MARVEL
Projeto da marvel e tudo que eu usei.
<!DOCTYPE html>
<html>
<head>
	<title>Personagens Marvel</title>
    <link rel="icon" href="logoMenorMarvel.PNG">

    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" type="text/css" href="estiloCssMarvel.css">
    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="css/bootstrap.min.css">
	  <!-- FONTAWESOME -->
    <link rel="stylesheet" type="text/css" href="fontawesome/css/all.css">
    <!-- MODO DE UTILIZAÇÃO fontawesome -> https://fontawesome.com/icons?d=gallery&m=free -->
	<!-- iconic -->
	<link rel="stylesheet" type="text/css" href="iconic/font/css/open-iconic-bootstrap.css">
	<!-- MODO DE UTILIZAÇÃO iconic -> https://useiconic.com/open/ -->
	
</head>
<body>
<header class="fixed-top">
    <nav class="navbar navbar-expand-md">
        <div class="container">
            <div class=" text-light d-flex col align-items-center col-4"> 
            <img style="width: 120px; height: 40px;" src="logoMarvel.PNG">
            </div>
        <button class=" btn btn-outline-dark navbar-toggler text-white" data-toggle="collapse"
        data-target="#icone">
            <i class="fas fa-bars"></i>
        </button>
        <div class="collapse navbar-collapse" id="icone">
           <ul class="navbar-nav ml-auto">
                <li class="divisor d-none d-md-inline-block"></li>
                <li class="nav-items"><a href="https://www.marvel.com/characters" class="nav-link">Ver mais no Site Oficial</a></li>
            </ul>
        </div>
    </div>
    </nav>
</header>
<section id="caixa" class="d-flex">
    <div class="container align-self-center">
        <!-- INICIO CAROUSEL -->
        <div class="carousel slide" data-ride="carousel" id="controle">
            <div class="carousel-inner">
                <!-- carousel1 -->
                <div class="carousel-item active">
                    <div class="row justify-content-center">
                    <div class="col-md-12"> <h1 class="display-2"> <b style="background: rgba(255,0,0,0.4); color: white; border-radius: 40px;"> PERSONAGENS DA MARVEL </b></h1></div>
                     
                    </div>
                </div>
         <!-- carousel2 -->
           <div class="carousel-item">
                <div class="row justify-content-center">
                    <div class="col-md-12"> <h1 class="display-1"> </h1></div>
                    <div class="col-lg-8 ">
                    <div class="row justify-content-center">
                        <div class="col-md-6 link"><a href="" class="btn btn-lg text-white" style="border-radius: 100px; background: rgba(255,0,0,0.4);"> "Fique viciado em uma ajuda calorosa de heróis e vilões da humilde Casa das Ideias!" </a></div>
                        </div>
                    </div>
                </div>
            </div>
         </div>
         <a href="#controle" class="carousel-control-prev" data-slide="prev"><span class="carousel-control-prev"><i class="fas fa-angle-left display-4"></i>"></span></a>  <!-- control-prev eu idico o modelo de controle, previo, anterior, data-slide eu falo o que quero que apareça no controle. -->
         <!--indico o icone que quero que seja o botão para controlar.-->
         <a href="#controle" class="carousel-control-next" data-slide="next"><span class="carousel-control-next"><i class="fas fa-angle-right display-4"></i></span></a>  <!-- control-prev eu idico o modelo de controle, previo, anterior, data-slide eu falo o que quero que apareça no controle. -->
         <!--indico o icone que quero que seja o botão para controlar.-->
        </div><!-- FIM CAROUSEL  -->

    </div>
</section>

<!--Seção responsável por listar os personagens-->
    <section id="caixa1">
        <div class="container">
           <div id = 'herois' 
                    style="
                    display: flex;
                    flex-wrap: wrap; 
                    justify-content: space-between; ">
            </div><!--fechamento div id herois-->
            
        </div> <!--fechamento div class container-->
    </section>

<!-- JAVASCRIPT -->
     <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
    <script src="js/bootstrap.min.js"></script>
   
<!----------IMPLEMENTANDO A API MARVEL---------->

    <script type="text/javascript">
    
    //criei a constante que recebe a minha timeStamp que foi geradapela seguinte fórmula: Math.floor(Date.now()/1000) utilizei essa formula no console do site que criei minha md5 e tive o seguinte resultado:
    const timeStamp = '1622056617';

    //aqui é minha chave pública
    const apikey = '2ec445bb84e58ff87f9ac79e403df3eb';

    //minha md5 foi criada neste site: "https://blueimp.github.io/JavaScript-MD5/" e precisei colocar tudo junto nesta ordem: timestamp+chavePrivada+chavePública
    const md5 = 'f58f113aa05d3b1a8c814064c6410950';

    //optei por verificar se a imagem do herói aparecia, então criei essa constante com o link da imagem que aparecia quando não tinha a imagem do heroi
    const imageNotFound = "http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available";

//o fetch é responsável por buscar no endereço da Marvel (por isso eu coloquei characters, para buscar somente os heróis) 
//Para ter acesso à API da Marvel eu utilizei o link exemplo mostrado no site da mesma e coloquei minha timestamp, minha chave pública e também a hash
//em seguida estipulei como limite de personagens o numero de 16 (que devido à futura verificação de existência imagens é reduzido para 12)
//o then é responsável por pegar apenas a parte json(que é a que me interessa) e colocar na variável respostaDoFetch

    fetch(`http://gateway.marvel.com/v1/public/characters?ts=${timeStamp}&apikey=${apikey}&hash=${md5}&limit=16`).then((respostaDoFetch) => {
        return respostaDoFetch.json();
        }).then((jsonParsed) => {
        const divHero = document.querySelector('#herois');
        //querySelector é responsável por selecionar a partir de uma tag. Neste caso, o id herois que está contido em uma div ´por enquanto vazia 

        //jsonParsed.data.results é o endereço que dá acesso a cada heroi e em seguida através do forEach eu coloco cada heroi momentaneamente na variavel element, então ao me referir a element no forEach, estarei me referindo àquele herói especifico daquele momento de repetição.
        //(consegui localizar este endereço através do console)
        jsonParsed.data.results.forEach(element => {

            if (element.thumbnail.path === imageNotFound ) {
                
            }else{
                const imagemHeroi = element.thumbnail.path + '.' + element.thumbnail.extension
                const nomeHeroi = element.name
                 apresentarHeroi(imagemHeroi, nomeHeroi, divHero);
            }

            //criei esse if para que só apareça na minha aplicação os personagens que tiverem imagem, então ao verificar que não tem imagem ele não adiciona, não faz nada apenas segue o código, para que no próximo forEach, ao verificar que tem imagem, ele caia no else, que adiciona estes endereços à variáveis que são enviadas como parametro para função criada abaixo

        });

        console.log(jsonParsed);
        //estou dando um console.log para que no console da minha aplicação seja possivel eu ver exatamente os personagens dentro do array que estão contidos e também os endereços para localizar inclusive as imagens, como já citado em alguns comentários anteriormente

    })//fechamento do segundo then 


    //aqui eu estou criando a função responsável por mostrar o heroi na div criada, para isso utilizei o createElement dos tipos div, texto e imagem
    function apresentarHeroi(imagemHeroi, nomeHeroi, divToAppend){

    const divPai = document.createElement('div')
    const divFilho = document.createElement('div')
    const nomeDoHeroi = document.createElement('text')
    const img = document.createElement('img')

    nomeDoHeroi.textContent = nomeHeroi
    img.src = imagemHeroi

    //estou inserindo a variavel img (que eu acabei de criar e é do tipo imagem) na divFilho
    divFilho.appendChild(img)

    //estou inserindo nomeDoHeroi (que eu criei acima e é do tipo texto) na divFilho
    divFilho.appendChild(nomeDoHeroi)

    //estou acessando a divPai e inserindo nela a divFilho
    divPai.appendChild(divFilho)

    //aqui eu estou acessando divToAppend e inserindo nela todos os conteúdos contidos na div pai
    divToAppend.appendChild(divPai)

    //aqui eu estou adicionando na divPai a class "personagem", criada no estiloCssMarvel para que siga um estilo e tamanho padronizado
    divPai.classList.add("personagem");
}



</script>

<footer>
        
            <div class="container ">
            <div class="row align-items-center">
                <div class=" text-light col-lg-2 d-flex"> 
               <img style="width: 150px; height: 50px;" src="logoMarvel.PNG">
                </div>
               

                <div class="col-md-3" >
                    Desenvolvedora responsável: Mariana Luiza
                </div>

                 <div class="col-md-3" >
                     Para mais informações sobre criação ou contato com a responsável, acesse os links ao lado:
                </div>

                   <div class= "col-lg-4">
                   
                    <ul class="">
                       <li> <a href="https://www.linkedin.com/in/mariana-luiza-46bb641b7/"><i style="font-size: 35px;" class="fab fa-linkedin"></i></a></li>
                        <li><a href="https://www.facebook.com/mariana.luiza.165033"><i style="font-size: 35px;" class="fab fa-facebook-square"></i></a></li>
                        <li><a href="https://www.instagram.com/2001alves/"><i style="font-size: 35px;" class="fab fa-instagram"></i></a></li>
                    </ul>
                   </div>
                
            </div><!--Fechamento da div responsável pelo alinhamento centralizadod dos itens-->
        </div><!--Fechamento div container-->
</footer>
	
</body>
</html>
