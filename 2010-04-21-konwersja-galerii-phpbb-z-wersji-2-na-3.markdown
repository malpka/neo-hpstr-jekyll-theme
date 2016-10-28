---
layout: post
title: "Konwersja galerii phpBB z wersji 2 na 3"
date: 2010-04-21 12:53
comments: true
categories:
- Do zapamiętania
---
<p></p>
<pre>
update phpbb3_gallery_images p3
join phpbb_album p2 on CONCAT(p3.image_name, '.jpg') = p2.pic_filename
set p3.image_name_clean = p2.pic_title,
p3.image_desc = p2.pic_desc,
p3.image_user_id = p2.pic_user_id,
p3.image_username = p2.pic_username
p3.image_time = p2.pic_time
p3.image_view_count = p2.pic_view_count
ip3.mage_id = p2.pic_id 
</pre>
<p>
<p>Przy okazji kod do zmiany kodowania:</p>
<p></p>
<pre>
UPDATE `phpbb3_posts` SET post_text = REPLACE(post_text, 'Ăą', 'ń')
</pre>
<p>