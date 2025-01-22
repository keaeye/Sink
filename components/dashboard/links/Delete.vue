<script setup>
import { toast } from 'vue-sonner'

const props = defineProps({
  link: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['update:link'])

async function deleteLink() {
  await useAPI('/api/link/delete', {
    method: 'POST',
    body: {
      slug: props.link.slug,
    },
  })
  emit('update:link', props.link, 'delete')
  toast('Delete successful!')
}
</script>

<template>
  <AlertDialog>
    <AlertDialogTrigger as-child>
      <slot />
    </AlertDialogTrigger>
    <AlertDialogContent class="max-w-[95svw] max-h-[95svh] md:max-w-lg grid-rows-[auto_minmax(0,1fr)_auto]">
      <AlertDialogHeader>
        <AlertDialogTitle>你确定吗？</AlertDialogTitle>
        <AlertDialogDescription>
          这个操作不能被撤销。这将会永远从服务器删除你的短链！！！
        </AlertDialogDescription>
      </AlertDialogHeader>
      <AlertDialogFooter>
        <AlertDialogCancel>确认</AlertDialogCancel>
        <AlertDialogAction @click="deleteLink">
          Continue
        </AlertDialogAction>
      </AlertDialogFooter>
    </AlertDialogContent>
  </AlertDialog>
</template>
