---
  <div class="card-reveal">
    <form class="col s12" action="https://formspree.io//{{site.user_email}}" method="POST">
      <div class="row">
        <div class="input-field col s6">
          <i class="material-icons prefix">account_circle</i>
          <input class="validate" id="icon_prefix" type="text" name="name">
          <label for="icon_prefix">Nome</label>
        </div>
        <div class="input-field col s6">
          <i class="material-icons prefix">email</i>
          <input class="validate" id="email" type="email" name="_replyto">
          <label for="email" data-error="Please enter a valid Email Address" data-success="Verified!">Email</label>
        </div>
      </div>
      <div class="row">
       <div class="input-field col s12">
         <i class="material-icons prefix">message</i>
         <textarea id="icon_prefix2" class="materialize-textarea" name="message"></textarea>
         <label for="icon_prefix2">Mensagem</label>
       </div>
     </div>
      <button class="btn waves-effect grey waves-dark darken-3 white-text z-depth-4" type="submit" name="action">Enviar
         <i class="material-icons right">send</i>
       </button>
    </form>
