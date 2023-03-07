<script>
export default {
    name: "AboutUs",
};
</script>

<template>
    <body>
        <div class="container my-container">
            <h1 class="title"></h1>
            <div class="row">
                <div class="col-lg-4 ">
                    <div class="card">
                        <div class="face front-face">
                            <img src="src\assets\img\marco (2).jpg" alt="" class="profile">
                            <div class="pt-3 text-uppercase name">
                                Sergio Marco Zanin
                            </div>
                            <div class="designation">Junior Full Stack Developer</div>
                        </div>
                        <div class="face back-face">
                            <span class="fas fa-quote-left"></span>
                            <div class="testimonial">
                                I made bacck the purchase price in just 48 hours! Thank you for making it pain less,
                                pleasant.
                                The service was execellent. I will refer everyone I know.
                            </div>
                            <span class="fas fa-quote-right"></span>
                            <div>
                                <a href="https://github.com/SergioMarcoZanin"><i class="fa-brands fa-github"></i></a>
                            </div>
                        </div>

                    </div>
                </div>
                <div class="col-lg-4">
                    <div class="card">
                        <div class="face front-face">
                            <img src="src\assets\img\Ele_foto_cv.jpeg" alt="" class="profile">
                            <div class="pt-3 text-uppercase name">
                                Eleonora Ruggieri
                            </div>
                            <div class="designation">Junior Full Stack Developer</div>
                        </div>
                        <div class="face back-face">
                            <span class="fas fa-quote-left"></span>
                            <div class="testimonial">
                                Really good, you have saved our business! I made bacck the purchase price in just 48 hours!
                                man, this thing is getting better and better as I learn more about it.
                            </div>
                            <span class="fas fa-quote-right"></span>
                            <div>
                                <a href="https://github.com/Iunora93"><i class="fa-brands fa-github"></i></a>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-lg-4">
                    <div class="card">
                        <div class="face front-face">
                            <img src="src\assets\img\IMG-20230213-WA0011.jpg" alt="" class="profile">
                            <div class="pt-3 text-uppercase name">
                                Valentina Riad
                            </div>
                            <div class="designation">Junior Full Stack Developer</div>
                        </div>
                        <div class="face back-face">
                            <span class="fas fa-quote-left"></span>
                            <div class="testimonial">
                                Account keeper is the most valuable business research we have EVER purchased. Without
                                electrician, we would ahave gone bankrupt by now.
                            </div>
                            <span class="fas fa-quote-right"></span>
                            <div>
                                <a href="https://github.com/Vale-riad"><i class="fa-brands fa-github"></i></a>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-lg-4">
                    <div class="card">
                        <div class="face front-face">
                            <img src="src\assets\img\fp.jfif" alt="" class="profile">
                            <div class="pt-3 text-uppercase name">
                                Nicola Gianfelici
                            </div>
                            <div class="designation">Junior Full Stack Developer</div>
                        </div>
                        <div class="face back-face">
                            <span class="fas fa-quote-left"></span>
                            <div class="testimonial">
                                Nel mondo sempre in evoluzione del Web Development la voglia di imparare e di accettare
                                nuove sfide non manca mai!
                                Mi piace accettarne ogni giorno di nuove e implementare così sempre più le mie conoscenze e
                                abilità.
                            </div>
                            <span class="fas fa-quote-right"></span>
                            <div>
                                <a href="https://github.com/32Fire32"><i class="fa-brands fa-github"></i></a>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-lg-4">
                    <div class="card">
                        <div class="face front-face">
                            <img src="src\assets\img\profile.jpg" alt="" class="profile">
                            <div class="pt-3 text-uppercase name">
                                Andrea De Lisi
                            </div>
                            <div class="designation">Junior Full Stack Developer</div>
                        </div>
                        <div class="face back-face">
                            <span class="fas fa-quote-left"></span>
                            <div class="testimonial">
                                Account keeper is the most valuable business research we have EVER purchased. Without
                                electrician, we would ahave gone bankrupt by now.
                            </div>
                            <span class="fas fa-quote-right"></span>
                            <div>
                                <a href="https://github.com/andreadldev"><i class="fa-brands fa-github"></i></a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </body>
</template>



<style lang="scss" scoped>
/* Reseting */
// * {
//     margin: 0;
//     padding: 0;
//     box-sizing: border-box;
//     font-family: 'Poppins', sans-serif;
// }

.my-container {
    padding-top: 100px;
}

body {
    background-color: rgb(253, 187, 45);

}


// .container {
//     margin-top: 100px;
//     margin-bottom: 100px;
// }

.container .col-lg-4 {
    display: flex;
    justify-content: center;
}



.testimonial {
    color: rgb(195, 34, 34);
}

.designation {
    color: rgb(195, 34, 34);
}

.fa-github {
    font-size: 50px;
    color: white;
    margin-top: 50px;
}

.card {
    width: 300px;
    height: 300px;
    transform-style: preserve-3d;
    perspective: 500px;
    border: none;
    background-color: inherit;
    margin-bottom: 55px;
}

.card .face {
    position: absolute;
    color: rgb(195, 34, 34);
    width: 100%;
    height: 100%;
    overflow: hidden;
    box-shadow: 0 15px 35px rgb(195, 34, 34);
    border-radius: 15px;
    transform-style: preserve-3d;
    transition: 1s;
    backface-visibility: hidden;
    border-top: 2px solid rgb(195, 34, 34);
    border-left: 2px solid rgb(195, 34, 34);
    /* border-right: 1px solid #999;
border-bottom: 1px solid #999; */
}

.card .face.front-face,
.card .face.back-face {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.card .face.front-face .profile {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    object-fit: cover;
}

.card .face.front-face .name {
    letter-spacing: 2px;
}

.card .face.front-face .designation {
    font-size: 0.8rem;
    color: rgb(195, 34, 34);
    ;
    letter-spacing: 0.8px;
}

.card:hover .face.front-face {
    transform: rotateY(180deg);
}

.card .face.back-face {
    position: absolute;
    background: rgba(255, 255, 255, 0.06);
    transform: rotateY(180deg);
    padding: 20px 30px;
    text-align: center;
    user-select: none;
}

.card .face.back-face .fa-quote-left {
    position: absolute;
    top: 25px;
    left: 25px;
    font-size: 1.2rem;
}

.card .face.back-face .fa-quote-right {
    position: absolute;
    bottom: 35px;
    right: 25px;
    font-size: 1.2rem;
}

.card:hover .face.back-face {
    transform: rotateY(360deg);
}

@media(min-width: 800px) {
    .title {
    padding-top: 50px;
    padding-bottom: 50px;
    text-align: center;
    color: rgb(195, 34, 34);
}
    .col-lg-4 {
        margin-top: 30px;
        margin-bottom: 20px;
    }
}
</style>
