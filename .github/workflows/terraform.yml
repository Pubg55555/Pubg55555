<?php

// تعيين التوكن الخاص بالبوت
$bot_token = '6125692974:AAFZZl2ZIGrUfkKZO0VSHuHxu43Bml1Z8bQ';

// تعيين معرف المستخدم لصاحب البوت
$owner_id = '5216030434';

// تعيين عنوان القناة المستلمة
$channel = '@binencid';

// تحديد الاستجابة المفتاحية
$update = json_decode(file_get_contents('php://input'), true);
if (isset($update['callback_query'])) {
    $callback_query = $update['callback_query'];
    $chat_id = $callback_query['message']['chat']['id'];
    $message_id = $callback_query['message']['message_id'];
    $data = $callback_query['data'];
    process_callback($data, $chat_id, $message_id);
} elseif (isset($update['message'])) {
    $message = $update['message'];
    $chat_id = $message['chat']['id'];
    $text = $message['text'];
    process_message($text, $chat_id);
}

// تعريف الأزرار
$buttons = [
    ['سحب المبلغ', 'ايداع المبلغ', 'حسابي'],
    ['عنوان المحفظة', 'دعوة الأصدقاء', 'مالك البوت'],
];

// إنشاء لوحة المفاتيح
$keyboard = json_encode(['inline_keyboard' => $buttons]);

// تحديث الرسالة الحالية
function update_message($text, $chat_id, $message_id, $keyboard)
{
    $data = [
        'chat_id' => $chat_id,
        'message_id' => $message_id,
        'text' => $text,
        'reply_markup' => $keyboard,
    ];
    $options = [
        'http' => [
            'method' => 'POST',
            'header' => 'Content-type: application/json',
            'content' => json_encode($data),
        ],
    ];
    $context = stream_context_create($options);
    $result = file_get_contents("https://api.telegram.org/bot$bot_token/editMessageText", false, $context);
}

// تحديد الاستجابة المفتاحية
$update = json_decode(file_get_contents('php://input'), true);
if (isset($update['callback_query'])) {
    $callback_query = $update['callback_query'];
    $chat_id = $callback_query['message']['chat']['id'];
    $message_id = $callback_query['message']['message_id'];
    $data = $callback_query['data'];
    process_callback($data, $chat_id, $message_id);
} elseif (isset($update['message'])) {
    $message = $update['message'];
    $chat_id = $message['chat']['id'];
    $message_id = $message['message_id']; // تعيين قيمة المتغير $message_id
    $text = $message['text'];
    process_message($text, $chat_id, $message_id); // تمرير المتغير $message_id كمعامل
}

// معالجة الرسائل النصية
function process_message($text, $chat_id, $message_id)
{
    global $keyboard;
    switch ($text) {
        case 'سحب المبلغ':
            $message = 'أدخل المبلغ المطلوب للسحب:';
            update_message($message, $chat_id, $message_id, $keyboard);
            break;
        case 'ايداع المبلغ':
            $message = 'أدخل المبلغ المطلوب للإيداع:';
            update_message($message, $chat_id, $message_id, $keyboard);
            break;
    }
}
 
