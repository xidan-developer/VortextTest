<script>
    import { Router, Link } from "svelte-routing";


</script>
<Router>
    <header class="header">
    <div class="container">
        <div class="d-flex align-items-center justify-between">
            <a href="/" class="header_logo">
                <svg width="98" height="32" viewBox="0 0 98 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M48.572 28.044H44.432V11.844H48.572V28.044ZM44 6.012C44 4.572 45.152 3.6 46.592 3.6C47.852 3.6 48.968 4.572 48.968 6.012C48.968 7.596 47.852 8.604 46.592 8.604C45.116 8.604 44 7.596 44 6.012ZM53.432 21.888V7.344H57.572V11.844H62.792V15.732H57.572V21.636C57.572 23.58 58.22 24.552 59.516 24.552C60.344 24.552 61.172 24.228 62 23.616L63.26 26.82C61.964 27.864 60.38 28.404 58.472 28.404C54.908 28.404 53.432 26.208 53.432 21.888ZM78.812 23.508L80 26.424C78.416 27.756 76.364 28.44 73.808 28.44C71.18 28.44 69.092 27.648 67.472 26.1C65.888 24.552 65.096 22.5 65.096 19.944C65.096 17.532 65.888 15.516 67.436 13.896C68.984 12.276 71.072 11.448 73.664 11.448C75.788 11.448 77.624 12.168 79.1 13.572C80.576 14.976 81.332 16.776 81.332 18.972C81.332 19.872 81.26 20.628 81.08 21.204H69.38C69.704 23.616 71.648 24.984 74.24 24.984C76.076 24.984 77.588 24.48 78.812 23.508ZM73.484 14.904C71.144 14.904 69.704 16.092 69.236 18.432H77.192C77.228 16.416 75.788 14.904 73.484 14.904ZM92.132 15.732H83.888V11.844H97.928V14.832L89.144 24.192H97.748V28.044H83.348V25.056L92.132 15.732ZM16 0C24.837 0 32 7.163 32 16C32 24.837 24.837 32 16 32C7.163 32 0 24.837 0 16C0 7.163 7.163 0 16 0ZM19.898 4.806L17.08 12.542C17.0676 12.576 17.0636 12.6124 17.0683 12.6482C17.073 12.6841 17.0863 12.7182 17.107 12.7479C17.1277 12.7775 17.1552 12.8017 17.1872 12.8184C17.2193 12.8352 17.2549 12.8439 17.291 12.844H22.622C22.6608 12.8441 22.699 12.8542 22.7327 12.8734C22.7665 12.8926 22.7947 12.9202 22.8146 12.9535C22.8346 12.9868 22.8455 13.0247 22.8465 13.0635C22.8474 13.1024 22.8383 13.1408 22.82 13.175L14.88 27.798C15.249 27.832 15.622 27.85 16 27.85C22.545 27.85 27.85 22.545 27.85 16C27.85 10.821 24.528 6.418 19.898 4.806ZM14.116 4.299C8.467 5.2 4.15 10.096 4.15 16C4.15 21.108 7.382 25.46 11.912 27.126L15.041 17.17C15.0515 17.1363 15.0539 17.1006 15.0481 17.0658C15.0423 17.031 15.0283 16.998 15.0074 16.9696C14.9865 16.9412 14.9591 16.9181 14.9276 16.9022C14.8961 16.8862 14.8613 16.878 14.826 16.878H10.31C10.2746 16.878 10.2396 16.8696 10.208 16.8535C10.1764 16.8374 10.1491 16.8141 10.1282 16.7854C10.1074 16.7568 10.0936 16.7236 10.088 16.6886C10.0824 16.6536 10.0851 16.6177 10.096 16.584L14.116 4.299Z" fill="#6A42E9"></path>
                </svg>
            </a>
            <nav class="header_nav">
                <ul class="d-flex align-items-center header_nav_list">
                    <li class="header_nav_list_item">
                        <Link to="/partners" class="header_nav_list_item__urls">Partners</Link>
                    </li>
                    <li class="header_nav_list_item">
                        <Link to="/integration" class="header_nav_list_item__urls">Integration</Link>
                    </li>
                    <li class="header_nav_list_item">
                        <Link to="/Company" class="header_nav_list_item__urls">Company</Link>
                    </li>
                    <li class="header_nav_list_item">
                        <Link to="/Support" class="header_nav_list_item__urls">Support</Link>
                    </li>
                    <li class="header_nav_list_item">
                        <Link to="/News" class="header_nav_list_item__urls">News</Link>
                    </li>
                </ul>
            </nav>
            <a class="header_sign">
                Sign in
            </a>
        </div>
    </div>

</header>

</Router>

<style lang="sass">
  $color-primary: #6a42e9
  .header
    margin-top: 40px
    &_sign
      color: $color-primary
      border: 1px solid $color-primary
      padding: 10px 30px
      border-radius: 10px
      &:hover
        background: $color-primary
        color: white
    &_nav
      &_list
        gap: 35px
        &_item
            &__urls:hover
              color: $color-primary

</style>