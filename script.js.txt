document.addEventListener("DOMContentLoaded", () => {

const featureBlocks = document.querySelectorAll('.feature-block');
const visualStates = document.querySelectorAll('.visual-state');

// ใช้ Intersection Observer เพื่อเช็คว่าผู้ใช้เลื่อน Scroll มาถึง Feature Block ข้อไหน
const observerOptions = {
    root: null,
    rootMargin: '-40% 0px -40% 0px', // ตรวจจับเมื่อ Element อยู่ตรงกลางๆ จอ
    threshold: 0
};

const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            // 1. ทำไฮไลท์ข้อความฝั่งซ้าย
            featureBlocks.forEach(block => block.classList.remove('active'));
            entry.target.classList.add('active');

            // 2. ดึงค่า Data-step เพื่อไปอัปเดตภาพฝั่งขวา
            const step = entry.target.getAttribute('data-step');
            
            visualStates.forEach(state => {
                state.classList.remove('active');
            });
            
            // สั่งให้ภาพ (Mock UI) โชว์ตรงกับเนื้อหา
            const activeVisual = document.getElementById(`vis-${step}`);
            if(activeVisual) {
                activeVisual.classList.add('active');
            }
        }
    });
}, observerOptions);

// เริ่มสังเกตการณ์ทุก Feature Block
featureBlocks.forEach(block => {
    observer.observe(block);
});
});
