// ==UserScript==
// @name         Копирование имени
// @namespace    https://catwar.net/
// @version      1.1
// @description  Добавляет красивую кнопку копирования имени
// @author       Обожжённый Солнцем (1080554)
// @match        *://*.catwar.net/*
// @match        *://*.catwar.su/*
// @grant        none
// ==/UserScript==

(function () {
    'use strict';

    const copyIcon = `
    <svg viewBox="0 0 24 24" width="15" height="15">
        <path d="M9 9h10v10H9z"
              fill="none"
              stroke="currentColor"
              stroke-width="2"/>
        <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"
              fill="none"
              stroke="currentColor"
              stroke-width="2"/>
    </svg>`;

    const checkIcon = `
    <svg viewBox="0 0 24 24" width="15" height="15">
        <path d="M20 6L9 17l-5-5"
              fill="none"
              stroke="currentColor"
              stroke-width="2"/>
    </svg>`;


    function addButtons() {

        document.querySelectorAll(".cat_tooltip").forEach(tooltip => {

            if (tooltip.querySelector(".cw-copy-btn")) return;

            const link = tooltip.querySelector("a");

            if (!link) return;


            const btn = document.createElement("span");

            btn.className = "cw-copy-btn";

            btn.innerHTML = copyIcon;

            btn.title = "Скопировать имя";


            // оформление
            btn.style.display = "inline-flex";
            btn.style.alignItems = "center";
            btn.style.justifyContent = "center";

            btn.style.marginLeft = "5px";

            btn.style.width = "16px";
            btn.style.height = "16px";

            btn.style.cursor = "pointer";
            btn.style.userSelect = "none";

            btn.style.color = "#7b7b7b";

            btn.style.textDecoration = "none";

            btn.style.verticalAlign = "middle";

            btn.style.transition =
                "color .15s ease, transform .15s ease";


            // наведение
            btn.addEventListener("mouseenter", () => {
                btn.style.color = "#4d8cff";
                btn.style.transform = "scale(1.12)";
            });


            btn.addEventListener("mouseleave", () => {
                btn.style.color = "#7b7b7b";
                btn.style.transform = "scale(1)";
            });


            // копирование
            btn.onclick = async function(e) {

                e.preventDefault();
                e.stopPropagation();

                const name = link.textContent.trim();

                try {

                    await navigator.clipboard.writeText(name);

                    btn.style.color = "#43b047";
                    btn.innerHTML = checkIcon;


                    setTimeout(() => {

                        btn.style.color = "#7b7b7b";
                        btn.innerHTML = copyIcon;

                    }, 900);


                } catch (err) {

                    console.error("Ошибка копирования:", err);

                }

            };


            // вставка после u, чтобы не было подчёркивания
            const underline = link.closest("u");

            if (underline) {
                underline.after(btn);
            } else {
                link.after(btn);
            }

        });

    }


    addButtons();


    new MutationObserver(addButtons).observe(document.body, {
        childList: true,
        subtree: true
    });


})();
