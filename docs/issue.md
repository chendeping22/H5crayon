## src/utils/cache-app.ts 缓存问题

contacts_student_key 与 contacts_student_clazz_key 这两个 key 进行数据缓存时会加上用户与组织信息相关的后缀，切换组织时会存在多份缓存数据。同时还是存在特定情况下会写入类似「teacher_guardian_student_TEST2_contactsStudentundefinedund」这种包含获取不到 store 相关信息的错误后缀。
