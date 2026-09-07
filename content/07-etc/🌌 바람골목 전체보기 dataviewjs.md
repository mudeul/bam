---
```dataviewjs
const files = app.vault.getFiles();
const targetImages = files.filter(file => file.path.includes("04. 바람골목") && ["png", "jpg", "jpeg", "webp"].includes(file.extension) && !file.path.includes("전체보기"));
targetImages.sort((a, b) => b.stat.mtime - a.stat.mtime);

if (targetImages.length === 0) {
    dv.paragraph("04. 바람골목 폴더에 사진이 없습니다.");
} else {
    let html = '<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 5px; margin-top: 10px;">';
    for (let img of targetImages) {
        let path = app.vault.getResourcePath(img);
        html += '<div style="aspect-ratio: 1 / 1; overflow: hidden; border-radius: 0px; background-color: #f0f0f0;"><img src="' + path + '" style="width: 100%; height: 100%; object-fit: cover;"></div>';
    }
    html += '</div>';
    dv.el("div", html);
}
```

