document.addEventListener("DOMContentLoaded", () => {
  
  document.querySelectorAll('a[href^="#"]').forEach((anchor) => {
    anchor.addEventListener("click", function (e) {
      e.preventDefault();
      document.querySelector(this.getAttribute("href")).scrollIntoView({
        behavior: "smooth",
      });
    });
  });

 
  const form = document.getElementById("contactForm");
  const result = document.getElementById("result");

  form.addEventListener("submit", function (e) {
    e.preventDefault();

    
    const formData = new FormData(form);
    const object = Object.fromEntries(formData);
    const json = JSON.stringify(object);

   
    result.innerHTML = "Please wait, sending message...";
    result.style.color = "#333";

    fetch("https://api.web3forms.com/submit", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
      body: json,
    })
      .then(async (response) => {
        let json = await response.json();
        if (response.status == 200) {
          
          result.innerHTML =
            "Thank you! Your message has been sent successfully.";
          result.style.color = "green";
          form.reset(); 
          
          setTimeout(() => {
            result.innerHTML = "";
          }, 5000);
        } else {
          
          console.log(response);
          result.innerHTML = json.message;
          result.style.color = "red";
        }
      })
      .catch((error) => {
        console.log(error);
        result.innerHTML = "Something went wrong! Please try again later.";
        result.style.color = "red";
      });
  });
});
