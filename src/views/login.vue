<template>
 <div class="login">
     <a-card title="登陆" class="cardForm">
         <a-form
            :model="formState"
            name="basic"
            :label-col="{ span: 4 }"
            :wrapper-col="{ span: 20 }"
            autocomplete="off"
            @finish="onFinish"
        >
            <a-form-item
            label="用户名"
            name="username"
            :rules="[{ required: true, message: '请输入用户名!' }]"
            >
            <a-input v-model:value="formState.username" />
            </a-form-item>
            <a-form-item
            label="密码"
            name="password"
            :rules="[{ required: true, message: '请输入密码!' }]"
            >
            <a-input-password v-model:value="formState.password" />
            </a-form-item>
            <a-form-item :wrapper-col="{ offset: 4, span: 20 }">
                <a-button type="primary" html-type="submit">登陆</a-button>
            </a-form-item>
        </a-form>
     </a-card>
 </div>
</template>
<script lang="ts">
    import { defineComponent, reactive } from "vue"
    import { message } from "ant-design-vue"
    import { useRouter } from 'vue-router'
    interface FormState {
        username: string;
        password: string;
    }
    export default defineComponent({
        setup () {
            const router = useRouter()
            const formState = reactive<FormState>({
                username: '',
                password: ''
            });
            const onFinish = (value: FormState) => {
                const {password, username} = value;
                if (username === "jack" && password === "redballoon") {
                    message.success("登陆成功");
                    setTimeout(() => {
                        router.push({path: "/"});
                    }, 1000);
                } else {
                    message.error("用户名或密码错误");
                }
            }
            return {
                onFinish,
                formState
            }
        }
  })
</script>
<style scoped>
.login {
    width: 100vw;
    height: 100vh;
    display:flex;
    align-items: center;
    justify-content: center;
    background: #f3f3f3;
}
.cardForm {
    width:500px;
}
</style>