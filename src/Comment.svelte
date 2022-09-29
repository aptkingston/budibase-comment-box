<script>
  import Avatar from "./Avatar.svelte"
  import dayjs from "dayjs"
  import relativeTime from "dayjs/plugin/relativeTime"
  import localizedFormat from "dayjs/plugin/localizedFormat"
  dayjs.extend(relativeTime)
  dayjs.extend(localizedFormat)

  export let comment
  export let destroy
</script>

<div class="comment">
  <Avatar name={comment.name} email={comment.email} />
  <div class="body">
    <div class="title">
      <div class="name" title={comment.email}>
        {comment.name || comment.email}
      </div>
      <div class="date" title={dayjs(comment.timestamp).format("llll")}>
        {dayjs(comment.timestamp).fromNow()}
      </div>
      <div class="delete" on:click={destroy}>
        ✕
      </div>
    </div>
    <div class="text">
      {comment.message}
    </div>
  </div>
</div>

<style>
  .comment {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: flex-start;
    gap: 12px;
    background: var(--spectrum-global-color-gray-50);
    padding: 12px;
    border-radius: 16px;
    border: 1px solid var(--spectrum-global-color-gray-200);
  }
  .body {
    flex: 1 1 auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    gap: 2px;
  }
  .title {
    display: flex;
    flex-direction: row;
    align-items: flex-end;
    gap: 6px;
  }
  .name {
    font-weight: bold;
  }
  .date {
    color: var(--spectrum-global-color-gray-600);
    font-size: 12px;
    flex: 1 1 auto;
  }
  .delete {
    color:  var(--spectrum-global-color-gray-400);
    display: none;
    transition: color 130ms ease-out;
  }
  .delete:hover {
    cursor: pointer;
    color: var(--spectrum-global-color-blue-600);
  }
  .comment:hover .delete {
    display: block;
  }
  .text {
    word-wrap: anywhere;
  }
</style>

