<template>
    <div class="home-container">
        <div class="main-title">
            {{ mainTitle }}
        </div>
        <div class="main-description" v-text="mainDescription"></div>
        <div class="book-catagory-title">
            {{ bookCategoryTitle }}
        </div>
        <div class="caraousel">
            <Carousel :perPage="perPage" :navigationEnabled="navigationEnabled"
                :paginationEnabled="paginationEnabled"
            >
                <Slide v-for="(book, index) in books" :key="index">
                    <div class="card" @click="selectBook(book)">
                        <img class="card-image" :src="book.book_image"/>
                        <div class="book-title">{{ book.title }}</div>
                        <div class="book-author">{{ book.author }}</div>
                        <div class="book-publisher">{{ book.publisher }}</div>
                        <div class="book-ratings">{{ book.rating }} out of 5</div>
                    </div>
                </Slide>
            </Carousel>
        </div>
        <div class="book-details" v-if="selectedBook.title">
           <div class="left">
                <div class="book-title">{{ selectedBook.title }}</div>
                <div><img class="book-image" :src="selectedBook.book_image"/></div>
                <button class="button">Add to Favourites +</button>
           </div>
           <div class="right">
               <div class="book-author">{{ selectedBook.author }}</div>
                <div class="book-publisher">{{ selectedBook.publisher }}</div>
                <div class="book-description">{{ selectedBook.description }}</div>
            </div>
            <div class="close" @click="closeBookDetails">
                <img src="../assets/close.png" alt="close">
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
import { Carousel, Slide } from 'vue-carousel';

export default {
  name: 'HomeContainer',
  components: {
    Carousel,
    Slide,
  },
  data() {
    return {
      mainTitle: 'Bookshelf & Book Racks',
      mainDescription: `Lorem Ipsum is simply dummy text of the printing and typesetting industry. 
      Lorem Ipsum is simply dummy text of the printing and typesetting industry. 
      Lorem Ipsum is simply dummy text of the printing and typesetting industry.`,
      bookCategoryTitle: 'Hardcover Fiction',
      books: [],
      perPage: 4,
      navigationEnabled: true,
      paginationEnabled: false,
      selectedBook: {},
    };
  },
  created() {
    this.getBooks();
  },
  methods: {
    getBooks() {
      try {
        axios.get('books.json')
          .then((response) => {
            this.books = response.data.results.books;
          });
      } catch (error) {
        console.error(error);
      }
    },
    selectBook(book) {
      this.selectedBook = book;
    },
    closeBookDetails() {
      this.selectedBook = {};
    },
  },
};
</script>
<style lang="scss" scoped>
    @font-face {
        font-family: "Helvetica Neue LT W05_65 Medium";
        src: url('../fonts/Helvetica Neue LT 65 Medium.ttf');
    }
    @font-face {
        font-family: "Helvetica Neue LT W05_45 Light";
        src: url('../fonts/Helvetica Neue LT 45 Light.ttf');
    }
    @font-face {
        font-family: "Helvetica Neue LT W05_35 Thin";
        src: url('../fonts/Helvetica Neue LT 35 Thin.ttf');
    }
    .home-container {
        margin-top: 60px;
        .main-title {
            font-family: "Helvetica Neue LT W05_35 Thin";
            font-size: 64px;
            font-weight: 100;
            font-stretch: normal;
            font-style: normal;
            line-height: 1.125;
            letter-spacing: normal;
            color: #fff;
            padding-left: 50px;
            margin: 0 0 16px;
        }
        .main-description {
            font-family: "Helvetica Neue LT W05_45 Light";
            font-size: 16px;
            font-weight: 300;
            font-stretch: normal;
            font-style: normal;
            line-height: 1.38;
            letter-spacing: .4px;
            color: #fff;
            margin: 0;
            max-width: 460px;
            padding-left: 50px;
        }
        .book-catagory-title {
            font-family: "Helvetica Neue LT W05_65 Medium";
            font-size: 22px;
            font-weight: 500;
            font-stretch: normal;
            font-style: normal;
            line-height: 1.27;
            letter-spacing: normal;
            color: #ffffff;
            padding-left: 50px;
            margin-top: 80px;
            margin-bottom: 50px;
        }
        .caraousel {
            max-width: 1200px;
            margin: 0 auto;
            ::v-deep .VueCarousel-navigation-button {
                color: White;
            }
            ::v-deep .VueCarousel-inner {
                height: 475px !important;
                .VueCarousel-slide {
                    align-self: center;
                }
            }
            .card {
                position: relative;
                width: 284px;
                height: 429px;

                .card-image {
                    opacity: 0.8;
                    width: 284px;
                    height: 429px;
                }

                .book-title {
                    font-size: 18px;
                    font-weight: 500;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: 1.2;
                    letter-spacing: -.2px;
                    color: #fff;
                    max-width: 100%;
                    position: absolute;
                    bottom: 45px;
                    left: 10px;
                }
                .book-author {
                    font-size: 13px;
                    font-weight: 300;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: 1.4;
                    letter-spacing: .4px;
                    color: hsla(0,0%,100%,.9);
                    position: absolute;
                    bottom: 30px;
                    left: 10px;
                }
                .book-publisher {
                    font-size: 13px;
                    font-weight: 300;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: 1.4;
                    letter-spacing: .4px;
                    color: hsla(0,0%,100%,.9);
                    position: absolute;
                    bottom: 15px;
                    left: 10px;
                }
                .book-ratings {
                    background: #003366;
                    opacity: 0.90;
                    font-size: 16px;
                    font-weight: 400;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: normal;
                    letter-spacing: .2px;
                    position: absolute;
                    color: hsla(0,0%,100%,.9);
                    top: 0px;
                    right:0px;
                    padding: 0px 10px;
                }

                &:hover {
                    height: 475px;

                    .card-image {
                       height: 475px;
                    }
                }
            }
        }
        .book-details {
            margin-top: 40px;
            margin-left: 50px;
            display: flex;
            .left {
                width: 400px;
                margin-right: 50px;

                .book-title {
                    font-size: 40px;
                    font-weight: 100;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: 1.2;
                    letter-spacing: .6px;
                    color: #c3a572;
                    margin-bottom: 40px;
                    margin-top: 0;
                    max-width: 360px;
                    text-align: left;
                }
                .book-image {
                    width: 60px;
                    border-radius: 4px;
                    object-fit: cover;
                }

                .button {
                    padding: 15px 25px;
                    font-size: 24px;
                    text-align: center;
                    cursor: pointer;
                    outline: none;
                    color: #fff;
                    background-color: #29302d;
                    border: none;
                    border-radius: 15px;
                    margin-top: 50px;

                    &:hover {
                        background-color: #212221;
                    }
                    &:active {
                        background-color: #212221;
                        transform: translateY(4px);
                    }
                }
            }
            .right {
                width: 600px;
                .book-author {
                    font-size: 18px;
                    font-weight: 500;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: normal;
                    letter-spacing: normal;
                    color: #fff;
                    margin-bottom: 2px;
                }
                .book-publisher {
                    font-size: 14px;
                    font-weight: 300;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: 1.44;
                    letter-spacing: .43px;
                    color: hsla(0,0%,100%,.6);
                }
                .book-description {
                    font-family: Helvetica Neue LT W05_45 Light;
                    font-size: 14px;
                    font-weight: 300;
                    font-stretch: normal;
                    font-style: normal;
                    line-height: 1.36;
                    letter-spacing: .4px;
                    color: hsla(0,0%,100%,.7);
                    margin-top: 40px;
                    word-break: break-word;
                }
            }
            .close {
                width: 250px;
                img {
                    display: flex;
                    margin-left: auto;
                }
            }
        }
    }
</style>
