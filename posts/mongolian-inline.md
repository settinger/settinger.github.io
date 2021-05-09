---
layout: default
title: Mongolian inline testing
---

## Mongolian inline testing

Choose from the dropdown options to test different web layouts.

<style>
.demo.mn {
  height: 720px;
  border: 1px solid black;
  padding: 1em;
  margin: 3em;
  font-size: 1.8em;
}
.demo:not(.mn) {
  width: 720px;
  border: 1px solid black;
  padding: 1em;
  margin: 3em;
  font-size: 1.2em;
}
.mn {
  writing-mode: vertical-lr;
}
.ar,
.la {
  writing-mode: horizontal-tb;
}
span {
  display: inline-block;
}
.inline.mn.ttb,
.inline.la.ttb,
.inline.ar.btt {
  writing-mode: vertical-lr;
}
.inline.ar.ttb,
.inline.la.btt {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
}
.inline.mn.ltr {
  writing-mode: horizontal-tb;
}
.inline.mn.rtl {
  transform: rotate(180deg);
  writing-mode: horizontal-tb;
}
</style>

<div class="form">
  <label for="body-text-selector">Document body script</label>
  <select id="body-text-selector" name="bodytext">
    <option value="la" selected>Latin (LTR)</option>
    <option value="ar">Arabic (RTL)</option>
    <option value="mn">Mongolian (TTB)</option>
  </select>
</div>

<div class="form">
  <label for="inline-text-selector">Inline excerpts script</label>
  <select id="inline-text-selector" name="inlinetext">
    <option value="la">Latin</option>
    <option value="ar">Arabic</option>
    <option value="mn" selected>Mongolian</option>
  </select>
</div>

<div class="form">
  <label for="orientation-selector">Orientation of excerpts</label>
  <select id="orientation-selector" name="orientation">
    <option value="ttb" selected>Vertical (TTB)</option>
    <option value="ltr">Horizontal (LTR)</option>
    <option value="rtl">Horizontal (RTL)</option>
  </select>
</div>

<div class="form">
  <label for="length-selector">Length of inline excerpts</label>
  <input
    type="number"
    value="6"
    min="1"
    max="30"
    step="1"
    id="length-selector"
    name="length"
    style="width: 3em"
  />
</div>

<div class="form">
  <label for="alignment-selector" id="alignment-label">
    Alignment of inline excerpt:
  </label>
  <select id="alignment-selector" name="alignment">
    <option value="baseline" selected>Baseline</option>
    <option value="top">Top</option>
    <option value="middle">Middle</option>
    <option value="bottom">Bottom</option>
  </select>
</div>

<div id="mongolian-inline-demo"></div>
<script>
  const lipsumArabic = [
    `لكن لا بد أن أوضح لك أن كل هذه الأفكار المغلوطة حول استنكار  النشوة وتمجيد الألم نشأت بالفعل، وسأعرض لك التفاصيل لتكتشف حقيقة وأساس تلك السعادة البشرية، فلا أحد يرفض أو يكره أو يتجنب الشعور بالسعادة، ولكن بفضل هؤلاء الأشخاص الذين لا يدركون بأن السعادة لا بد أن نستشعرها بصورة أكثر عقلانية ومنطقية فيعرضهم هذا لمواجهة الظروف الأليمة، وأكرر بأنه لا يوجد من يرغب في الحب ونيل المنال ويتلذذ بالآلام، الألم هو الألم ولكن نتيجة لظروف ما قد تكمن السعاده فيما نتحمله من كد وأسي.`,
    `و سأعرض مثال حي لهذا، من منا لم يتحمل جهد بدني شاق إلا من أجل الحصول على ميزة أو فائدة؟ ولكن من لديه الحق أن ينتقد شخص ما أراد أن يشعر بالسعادة التي لا تشوبها عواقب أليمة أو آخر أراد أن يتجنب الألم الذي ربما تنجم عنه بعض المتعة ؟ `,
    `علي الجانب الآخر نشجب ونستنكر هؤلاء الرجال المفتونون بنشوة اللحظة الهائمون في رغباتهم فلا يدركون ما يعقبها من الألم والأسي المحتم، واللوم كذلك يشمل هؤلاء الذين أخفقوا في واجباتهم نتيجة لضعف إرادتهم فيتساوي مع هؤلاء الذين يتجنبون وينأون عن تحمل الكدح والألم . من المفترض أن نفرق بين هذه الحالات بكل سهولة ومرونة. في ذاك الوقت عندما تكون قدرتنا علي الاختيار غير مقيدة بشرط وعندما لا نجد ما يمنعنا أن نفعل الأفضل فها نحن نرحب بالسرور والسعادة ونتجنب كل ما يبعث إلينا الألم. في بعض الأحيان ونظراً للالتزامات التي يفرضها علينا الواجب والعمل سنتنازل غالباً ونرفض الشعور بالسرور ونقبل ما يجلبه إلينا الأسى. الإنسان الحكيم عليه أن يمسك زمام الأمور ويختار إما أن يرفض مصادر السعادة من أجل ما هو أكثر أهمية أو يتحمل الألم من أجل ألا يتحمل ما هو أسوأ. `,
    `و سأعرض مثال حي لهذا، من منا لم يتحمل جهد بدني شاق إلا من أجل الحصول على ميزة أو فائدة؟ ولكن من لديه الحق أن ينتقد شخص ما أراد أن يشعر بالسعادة التي لا تشوبها عواقب أليمة أو آخر أراد أن يتجنب الألم الذي ربما تنجم عنه بعض المتعة ؟ `,
    `علي الجانب الآخر نشجب ونستنكر هؤلاء الرجال المفتونون بنشوة اللحظة الهائمون في رغباتهم فلا يدركون ما يعقبها من الألم والأسي المحتم، واللوم كذلك يشمل هؤلاء الذين أخفقوا في واجباتهم نتيجة لضعف إرادتهم فيتساوي مع هؤلاء الذين يتجنبون وينأون عن تحمل الكدح والألم .`,
  ];
  // Arabic text from: https://istizada.com/arabic-lorem-ipsum/
  const lipsumLatin = [
    `Lorem ipsum dolor sit amet, eu eam modus aliquando, has te tempor iriure civibus, ex aeque simul nostrud nam. Graece sapientem sadipscing et mel, ut est omnes aperiam epicuri. Has at probo illum, quod impedit rationibus ut quo. At sea sanctus delicata explicari, eos id denique scriptorem. Pro ut doctus veritus.`,
    `No modus deterruisset sed. Sumo dictas complectitur ex pro. Eum ut virtute consulatu, quo dico minimum menandri no, ferri primis sed no. Labore semper ponderum no pro, labore singulis usu cu. Solet nonumes neglegentur ne vis. Sed alii admodum epicurei no, est virtute antiopam in, id nam tibique gubergren.`,
    `Pro diam nibh omittam te. In justo paulo legere nam, cum ad omnis regione expetendis, pri ad aeterno periculis eloquentiam. Eos quem veritus ceteros et, tale adhuc persequeris mel in, oratio eruditi tacimates vis an. Sea ne expetenda deseruisse scribentur. Cu pro posse iudico, sea eu agam nusquam. Soluta electram te vis, no vel sint dicam minimum.`,
    `Tale autem in cum, vis liber clita propriae ex, cu pri possim repudiandae. Erant rationibus et eum, ex quo oporteat nominati interpretaris. Ea tibique albucius percipit has, id eam euismod accusamus vituperata. Ius ea sint consectetuer, quo essent persius deterruisset ea.`,
    `Modo vocent malorum no sed, nam in labores conceptam, vis magna facer dicunt cu. Ne per graecis pertinax. Inimicus efficiantur an per, autem fabulas consequuntur nec in, duo ei solum sanctus reprimique. Mel et simul disputationi. Eu per vidit audiam.`,
  ];
  const lipsumMongolian = [
    `ᠵᠣᠭᠠᠴᠠᠯ ᠦᠨ ᠭᠠᠵᠠᠷ ᠬᠦᠴᠦᠷᠬᠡᠭᠯᠡᠨ ᠨᠦᠵᠢᠳᠯᠡᠭᠰᠡᠨ ᠬᠡᠷᠡᠭ ᠭᠠᠷᠪᠠ`,
    `ᠣᠢᠷ᠎ᠠ ᠵᠢᠨ ᠡᠳᠦᠷ᠂ ᠦᠪᠦᠷ ᠮᠣᠩᠭᠣᠯ ᠦᠨ ᠰᠢᠯᠢ ᠵᠢᠨ ᠭᠣᠣᠯ ᠠᠢᠮᠠᠭ ᠦᠨ ᠰᠢᠯᠣᠭᠣᠨ ᠬᠦᠬᠡ ᠬᠣᠰᠢᠭᠣᠨ ᠦ ᠰᠢᠭᠦᠬᠦ ᠬᠣᠷᠢᠶ᠎ᠠ ᠨᠢᠭᠡᠨ ᠬᠦᠴᠦᠷᠬᠡᠭᠯᠡᠨ ᠨᠦᠵᠢᠳᠯᠡᠭᠰᠡᠨ ᠶᠠᠯᠠᠲᠣ ᠬᠡᠷᠡᠭ ᠲᠦ ᠰᠢᠭᠦᠯᠲᠡ ᠬᠢᠪᠡ᠃ ᠰᠢᠭᠦᠨ ᠲᠠᠰᠣᠯᠣᠯᠳᠠ ᠪᠠᠷ᠂ ᠵᠠᠭᠠᠯᠳᠣᠭᠳᠠᠭᠴᠢ ᠡᠷᠬᠢᠮᠲᠦ ᠵᠢ ᠬᠦᠴᠦᠷᠭᠡᠭᠯᠡᠨ᠂ ᠨᠦᠵᠢᠳᠯᠡᠭᠰᠡᠨ ᠶᠡᠯ᠎ᠡ ᠪᠡᠷ ᠭᠣᠷᠪᠠᠨ ᠵᠢᠯ ᠦᠨ ᠬᠣᠭᠣᠴᠠᠭ᠎ᠠ ᠲᠠᠢ ᠬᠣᠷᠢᠬᠣ ᠡᠷᠡᠭᠦᠦ ᠪᠡᠷ ᠰᠢᠳᠬᠡᠭᠰᠡᠨ ᠪᠠᠢᠨ᠎ᠠ᠃`,
    `ᠵᠠᠭᠠᠯᠳᠣᠭᠳᠠᠭᠴᠢ ᠡᠷᠬᠢᠮᠲᠦ ᠪᠣᠯ ᠰᠢᠯᠢ ᠵᠢᠨ ᠭᠣᠣᠯ ᠠᠢᠮᠠᠭ ᠦᠨ ᠰᠢᠯᠣᠭᠣᠨ ᠬᠦᠬᠡ ᠬᠣᠰᠢᠭᠣᠨ ᠦ ᠬᠦᠮᠦᠨ᠂ ᠨᠢᠭᠡᠨ ᠡᠳᠦᠷ ᠲᠡᠭᠦᠨ ᠦ ᠪᠡᠭᠡᠵᠢᠩ ᠳᠤ ᠠᠵᠢᠯᠯᠠᠵᠤ ᠪᠠᠢᠭ᠎ᠠ ᠨᠠᠢᠵᠠ ᠴᠣᠯᠮᠣᠨ ᠨᠢ ᠠᠮᠠᠷᠠᠯᠲᠠ ᠪᠠᠷ ᠵᠣᠭᠠᠴᠠᠷ᠎ᠠ ᠢᠷᠡᠵᠡᠢ᠃ ᠬᠠᠮᠲᠣ ᠢᠷᠡᠭᠰᠡᠨ ᠨᠢ ᠪᠠᠰᠠ ᠴᠣᠯᠮᠣᠨ ᠦ ᠡᠮᠡᠭᠲᠡᠢ ᠨᠠᠢᠵᠠ ᠰᠠᠷᠠᠨ᠎ᠠ ᠪᠠᠢᠵᠠᠢ᠃ ᠡᠷᠬᠢᠮᠲᠦ ᠨᠠᠢᠵᠠ ᠴᠣᠯᠮᠣᠨ᠂ ᠰᠠᠷᠠᠨ᠎ᠠ ᠬᠣᠶᠠᠷ ᠢ ᠲᠣᠰ ᠬᠣᠰᠢᠭᠣᠨ ᠦ ᠨᠢᠭᠡᠨ ᠵᠣᠭᠠᠴᠠᠯ ᠦᠨ ᠭᠠᠵᠠᠷ ᠳᠠᠭᠠᠭᠣᠯᠣᠨ ᠬᠦᠷᠴᠦ᠂ ᠮᠣᠩᠭᠣᠯ ᠭᠡᠷ ᠲᠦ ᠠᠷᠢᠬᠢ ᠮᠢᠬ᠎ᠠ ᠭᠠᠷᠠᠭᠠᠨ ᠵᠣᠴᠢᠯᠠᠵᠤ ᠳᠡᠢᠯᠡᠵᠦ ᠬᠠᠷᠠᠩᠭᠣᠢ ᠪᠣᠯᠬᠣ ᠳᠤ᠂ ᠰᠠᠷᠠᠨ᠎ᠠ ᠪᠠᠬᠠᠨ ᠰᠣᠭᠳᠣᠭᠰᠠᠨ ᠪᠣᠯᠬᠣᠷ᠂ ᠬᠠᠵᠠᠭᠣ ᠵᠢᠨ ᠮᠣᠩᠭᠣᠯ ᠭᠡᠷ ᠲᠦ ᠣᠷᠣᠵᠣ ᠣᠨᠲᠠᠭᠰᠠᠨ ᠪᠠᠢᠨ᠎ᠠ᠃ ᠡᠷᠬᠢᠮᠲᠦ ᠪᠠ ᠴᠣᠯᠮᠣᠨ ᠬᠣᠶᠠᠭᠤᠯᠠ ᠪᠠᠬᠠᠨ ᠠᠷᠢᠬᠢ ᠣᠣᠭᠣᠵᠣ ᠪᠠᠢᠭᠠᠳ᠂ ᠡᠷᠬᠢᠮᠲᠦ ᠪᠡᠶ᠎ᠡ ᠵᠠᠰᠠᠬᠤ  ᠪᠠᠷ ᠭᠠᠷᠴᠣ ᠢᠷᠡᠭᠡᠳ᠂ ᠬᠠᠵᠠᠭᠣ ᠵᠢᠨ ᠮᠣᠩᠭᠣᠯ ᠭᠡᠷ ᠲᠦ ᠰᠢᠷᠭᠣᠨ ᠣᠷᠣᠭᠠᠳ ᠦᠭᠡ ᠳᠠᠭᠣᠨ ᠦᠭᠡᠢ ᠪᠡᠷ ᠰᠢᠭᠣᠳ ᠣᠨᠲᠠᠵᠤ ᠪᠠᠢᠭᠰᠠᠨ ᠰᠠᠷᠠᠨ᠎ᠠ ᠲᠠᠢ ᠪᠡᠯᠭᠡ ᠵᠢᠨ ᠠᠵᠢᠯᠯᠠᠭ᠎ᠠ ᠬᠢᠵᠦ ᠡᠬᠢᠯᠡᠵᠡᠢ᠃ ᠮᠣᠩᠭᠣᠯ ᠭᠡᠷ ᠲᠦ ᠳ᠋ᠧᠩ ᠦᠭᠡᠢ ᠬᠠᠷᠠᠩᠭᠣᠢ ᠪᠠᠢᠭᠰᠠᠨ ᠪᠣᠯᠬᠣᠷ᠂ ᠰᠠᠷᠠᠨ᠎ᠠ ᠦᠪᠡᠷ ᠦᠨ ᠡᠷᠡᠭᠲᠡᠢ ᠨᠠᠢᠵᠠ ᠴᠣᠯᠮᠣᠨ ᠭᠡᠵᠦ ᠡᠨᠳᠡᠭᠦᠷᠡᠭᠡᠳ ᠳᠣᠣᠭᠠᠷᠣᠭᠰᠠᠨ ᠦᠭᠡᠢ᠂ ᠭᠡᠨᠡᠳᠲᠡ ᠭᠠᠷ ᠲᠣ ᠨᠢ ᠣᠷᠲᠣ ᠰᠢᠭ ᠦᠰᠦᠲᠡᠢ ᠬᠦᠮᠦᠨ ᠲᠡᠮᠲᠡᠷᠢᠭᠳᠡᠵᠦ᠂ ᠴᠣᠯᠮᠣᠨ ᠪᠣᠯ ᠣᠬᠣᠷ ᠦᠰᠦᠲᠡᠢ ᠲᠣᠯᠠ ᠰᠠᠷᠠᠨ᠎ᠠ ᠰᠠᠨᠳᠣᠷᠣᠨ ᠬᠠᠰᠬᠢᠷᠣᠭᠰᠠᠨ ᠳᠤ᠂ ᠴᠣᠯᠮᠣᠨ ᠬᠠᠵᠠᠭᠣ ᠵᠢᠨ ᠮᠣᠩᠭᠣᠯ ᠭᠡᠷ ᠡᠴᠡ ᠣᠷᠣᠵᠣ ᠢᠷᠡᠭᠡᠳ᠂ ᠳᠠᠷᠣᠢ ᠬᠡᠷᠡᠭ ᠮᠡᠳᠡᠭᠦᠯᠦᠭᠰᠡᠨ ᠪᠠᠢᠨ᠎ᠠ᠃`,
    `ᠮᠠᠨ ᠦ ᠣᠯᠣᠰ ᠦᠨ ᠡᠷᠡᠭᠦᠦ ᠵᠢᠨ ᠬᠠᠣᠯᠢ ᠵᠢᠨ ᠲᠣᠭᠲᠠᠭᠠᠯ ᠵᠢᠡᠷ᠂ ᠬᠦᠴᠦᠷᠬᠡᠭᠯᠡᠨ ᠨᠦᠵᠢᠳᠯᠡᠭᠰᠡᠨ ᠶᠠᠯ᠎ᠠ ᠭᠡᠳᠡᠭ ᠨᠢ ᠡᠮᠡᠭᠲᠡᠢ ᠵᠢᠨ ᠵᠣᠷᠢᠭ ᠰᠠᠨᠠᠭᠠᠨ ᠡᠴᠡ ᠵᠦᠷᠢᠴᠡᠨ ᠂ ᠬᠦᠴᠦᠷᠬᠡᠭᠯᠡᠯ᠂ ᠰᠦᠷᠳᠡᠭᠦᠯᠦᠯ ᠪᠣᠶᠣ ᠪᠣᠰᠣᠳ ᠠᠷᠭ᠎ᠠ ᠪᠠᠷᠢᠯ ᠵᠢᠡᠷ ᠡᠮᠡᠭᠲᠡᠢ ᠲᠡᠢ ᠪᠡᠯᠭᠡ ᠵᠢᠨ ᠬᠠᠷᠢᠴᠠᠭ᠎ᠠ ᠡᠭᠦᠰᠬᠦ ᠠᠵᠢᠯᠯᠠᠭ᠎ᠠ ᠵᠢ ᠵᠢᠭᠠᠵᠤ ᠪᠣᠢ᠃ ᠲᠣᠰ ᠬᠡᠷᠡᠭ ᠲᠦ᠂ ᠵᠠᠭᠠᠯᠳᠣᠭᠳᠠᠭᠴᠢ ᠡᠷᠬᠢᠮᠲᠦ ᠰᠠᠷᠠᠨ᠎ᠠ ᠵᠢᠨ ᠠᠷᠢᠬᠢ ᠣᠣᠭᠣᠭᠰᠠᠨ ᠦ ᠳᠠᠷᠠᠭ᠎ᠠ᠂ ᠣᠶᠣᠨ ᠰᠡᠷᠡᠯ ᠪᠠᠯᠠᠷᠠᠬᠠᠢ ᠪᠠᠢᠳᠠᠯ ᠢ ᠵᠠᠪᠰᠢᠨ ᠪᠡᠯᠭᠡ ᠵᠢᠨ ᠬᠠᠷᠢᠴᠠᠭ᠎ᠠ ᠡᠭᠦᠰᠦᠭᠰᠡᠨ ᠨᠢ ᠶᠠᠯ᠎ᠠ ᠪᠦᠷᠢᠯᠳᠦᠬᠦ ᠨᠦᠬᠦᠴᠡᠯ ᠳᠡᠬᠢ ᠪᠣᠰᠣᠳ ᠠᠷᠭ᠎ᠠ ᠪᠠᠷᠢᠯ ᠳᠤ ᠬᠠᠷᠠᠭᠠᠯᠵᠠᠭᠰᠠᠨ ᠪᠦᠭᠡᠳ ᠰᠠᠷᠠᠨ᠎ᠠ ᠦᠪᠡᠷ ᠦᠨ ᠡᠷᠡᠭᠲᠡᠢ ᠨᠠᠢᠵᠠ ᠪᠢᠰᠢ ᠭᠡᠳᠡᠭ ᠢ ᠮᠡᠳᠡᠭᠰᠡᠨ ᠦ ᠳᠠᠷᠠᠭ᠎ᠠ ᠳᠠᠷᠣᠢ ᠬᠠᠰᠬᠢᠷᠣᠭᠰᠠᠨ ᠨᠢ ᠡᠮᠡᠭᠲᠡᠢ ᠵᠢᠨ ᠵᠣᠷᠢᠭ ᠰᠠᠨᠠᠭᠠᠨ ᠡᠴᠡ ᠵᠦᠷᠢᠴᠡᠪᠡ ᠭᠡᠳᠡᠭ ᠢ ᠬᠦᠢᠴᠡᠳ ᠬᠠᠷᠠᠭᠣᠯᠵᠣ ᠪᠢᠢᠨ᠎ᠠ᠃`,
    `※ ᠲᠣᠬᠠᠢ ᠵᠢᠨ ᠬᠦᠮᠦᠨ ᠦ ᠬᠣᠪᠢ ᠵᠢᠨ ᠨᠢᠭᠣᠴᠠ ᠵᠢ ᠬᠠᠮᠠᠭᠠᠯᠠᠬᠤ ᠵᠢᠨ ᠲᠦᠯᠦᠭᠡ ᠬᠡᠷᠡᠭ ᠲᠦ ᠬᠣᠯᠪᠣᠭᠳᠠᠭᠰᠠᠨ ᠬᠦᠮᠦᠨ ᠦ ᠨᠡᠷ᠎ᠡ ᠵᠢ ᠪᠣᠷᠣᠭᠣᠯᠠᠪᠠ᠃`,
    `ᠠᠳᠠᠳ ᠦᠨ ᠰᠦᠯᠵᠢᠶ᠎ᠡ ᠡᠴᠡ ᠰᠢᠯᠵᠢᠭᠦᠯᠦᠨ ᠨᠡᠢᠲᠡᠯᠡᠪᠡ᠃`,
  ];
  // Mongolian text from: http://www.cjvlang.com/mongol/misc03.html
  // Orientation options for Mongolian inline excerpts
  const orientationMn = `<option value="ttb" selected>Vertical (TTB)</option> <option value="ltr">Horizontal (LTR)</option> <option value="rtl">Horizontal (RTL)</option>`;
  // Orientation options for Latin inline excerpts
  const orientationLa = `<option value="ltr" selected>Horizontal (LTR)</option> <option value="ttb">Vertical (TTB)</option> <option value="btt">Vertical (BTT)</option>`;
  // Orientation options for Arabic inline excerpts
  const orientationAr = `<option value="rtl" selected>Horizontal (RTL)</option> <option value="ttb">Vertical (TTB)</option> <option value="btt">Vertical (BTT)</option>`;
  const $bodyText = document.getElementById("body-text-selector");
  let bodyVal = $bodyText.value;
  const $inlineText = document.getElementById("inline-text-selector");
  let inlineVal = $inlineText.value;
  const $orientation = document.getElementById("orientation-selector");
  let orientVal = $orientation.value;
  const $length = document.getElementById("length-selector");
  let lengthVal = parseInt($length.value);
  const $alignment = document.getElementById("alignment-selector");
  let bodyTextList = [];
  let inlineTextList = [];
  // Random integer selector
  const randomInt = (...args) => {
    if (args.length == 1) {
      return Math.floor(Math.random() * args[0]);
    } else if (args.length == 2) {
      return args[0] + Math.floor(Math.random() * (args[1] - args[0]));
    }
  };
  // Function to update list of body text paragraphs
  const updateBodyTextList = () => {
    bodyTextList =
      bodyVal == "la"
        ? lipsumLatin.slice()
        : bodyVal == "ar"
        ? lipsumArabic.slice()
        : lipsumMongolian.slice();
  };
  // Function to update list of inline texts (assume bodyTextList has already been populated)
  const updateInlineTextList = () => {
    let source =
      inlineVal == "la"
        ? lipsumLatin.slice()
        : inlineVal == "ar"
        ? lipsumArabic.slice()
        : lipsumMongolian.slice();
    source = source.join("").replace(" ", "");
    inlineTextList = bodyTextList.map((_) => {
      let start = randomInt(source.length - 31);
      return source.substring(start, start + 30);
    });
  };
  // Function to call to insert NEW spans (and remove old ones)
  const insertSpans = () => {
    // Remove any existing inline spans
    const inlines = document.querySelectorAll("span.inline");
    for (let inline of inlines) inline.remove();
    // Insert new inline spans
    const paragraphs = document.querySelectorAll("p.bodytext");
    for (let paragraph of paragraphs) {
      const insertionPoint = randomInt(10, paragraph.innerText.length - 10);
      paragraph.innerHTML =
        paragraph.innerText.substring(0, insertionPoint) +
        `<span class="${inlineVal} inline ${orientVal}"></span>` +
        paragraph.innerText.substring(insertionPoint);
    }
    return document.querySelectorAll("span.inline");
  };
  // Function to insert text into existing spans
  const updateSpans = () => {
    // Check if <span>s are already inserted into body paragraphs; if not, insert them
    let inlineSpans = document.querySelectorAll("span.inline");
    if (inlineSpans.length <= 0) {
      inlineSpans = insertSpans();
    }
    // Change language identifier class and inner text of spans
    for (let [index, inlineSpan] of inlineSpans.entries()) {
      inlineSpan.innerText = inlineTextList[index].substring(0, lengthVal);
      inlineSpan.className = `${inlineVal} inline ${orientVal}`;
    }
  };
  // Function to call to update orientation of inline spans
  const updateSpanOrientation = () => {
    let spans = document.querySelectorAll("span.inline");
    for (let span of spans) {
      span.className = `${inlineVal} inline ${orientVal}`;
    }
  };
  // Function to call when inline text selection changes
  const changeInline = () => {
    const newInlineVal = $inlineText.value;
    if (newInlineVal == inlineVal) return;
    inlineVal = newInlineVal;
    updateInlineTextList();
    updateSpans();
    // Update options in the orientation dropdown
    $orientation.innerHTML =
      inlineVal == "la"
        ? orientationLa
        : inlineVal == "ar"
        ? orientationAr
        : orientationMn;
    orientVal = $orientation.value;
    updateSpanOrientation();
  };
  // Function to generate body HTML (without inline texts)
  const renderBody = () => {
    const bodyText = `<div class="${bodyVal} demo"><p class="bodytext">${bodyTextList.join(
      `</p><p class="bodytext">`
    )}</p></div>`;
    document.getElementById("mongolian-inline-demo").innerHTML = bodyText;
  };
  // Function to call when alignment selector changes
  const changeAlignment = () => {
    let spans = document.querySelectorAll("span.inline");
    for (let span of spans) {
      span.style.verticalAlign = $alignment.value;
    }
  };
  // Function to call when body text selection changes
  // (Also forces a refresh of inline texts)
  const changeBody = () => {
    const newBodyVal = $bodyText.value;
    if (newBodyVal == bodyVal) return;
    bodyVal = newBodyVal;
    bodyTextList =
      bodyVal == "la"
        ? lipsumLatin.slice()
        : bodyVal == "ar"
        ? lipsumArabic.slice()
        : lipsumMongolian.slice();
    renderBody();
    updateInlineTextList();
    updateSpans();
    changeAlignment();
  };
  // Function to call when inline text length changes
  const changeLength = () => {
    const newLengthVal = parseInt($length.value);
    if (newLengthVal == lengthVal) return;
    lengthVal = newLengthVal;
    updateSpans();
  };
  // Function to call when inline orientation changes
  const changeOrientation = () => {
    const newOrientVal = $orientation.value;
    if (newOrientVal == orientVal) return;
    orientVal = newOrientVal;
    updateSpanOrientation();
  };
  $bodyText.oninput = changeBody;
  $inlineText.oninput = changeInline;
  $orientation.oninput = changeOrientation;
  $length.oninput = changeLength;
  $alignment.oninput = changeAlignment;
  window.onload = (e) => {
    updateBodyTextList();
    updateInlineTextList();
    renderBody();
    updateSpans();
  };
</script>