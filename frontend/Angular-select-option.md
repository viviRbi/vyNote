```
<select name="batch-name" *ngIf="theBatches" (change)="selectBatch()" [(ngModel)]="selectedBatchIdAndId">
  <option *ngFor="let batch of theBatches" value="{{batch.id}}|{{batch.batchId}}">{{batch.startDate}} {{ batch.location }} - {{batch.skill}}</option>
</select>

// value of option will be pass to Select and Select had 2 way data binding with selectedBatchAndId field
```